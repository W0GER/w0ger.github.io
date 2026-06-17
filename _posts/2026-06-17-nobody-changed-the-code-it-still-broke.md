---
title: "Nobody Changed the Code. It Still Broke."
comments: true
tags:
  - .NET
  - AWS Lambda
  - Debugging
  - Dependencies
  - Software Engineering
date: 2026-06-17 00:00:00.000000000 -05:00
excerpt: >-
  A production Lambda started crashing on startup with no code change behind it.
  The cause was a three-way collision between a new AWS runtime, an old bundled
  library, and a routine dependency upgrade — and the fix is a one-line lesson
  in scoping what you scan.
header:
  teaser: images/getty-images-fV_JINOCblA-unsplash-2.jpg
  overlay_image: images/getty-images-fV_JINOCblA-unsplash-2.jpg
  overlay_filter: 0.5
  caption: >-
    Photo by [**Getty Images**](https://unsplash.com/@gettyimages?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [**Unsplash**](https://unsplash.com/photos/a-hacker-in-military-unifrorm-on-dark-web-cyberwar-concept-fV_JINOCblA?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
categories:
  - Technology
  - Development
---

A function we hadn't touched in weeks suddenly refused to start.

No new business logic. No deploy carrying a behavior change. The same code
that had been running quietly in production for ages now fell over on cold
start, crashing before it could handle a single request. The logs pointed at
something deep in startup, and the first instinct — the wrong one — was to go
hunting through our own code for what we broke.

We didn't break anything. That's the unsettling part, and it's also the whole
story. The worst production bugs aren't the ones where someone shipped a bad
line. They're the ones where the ground shifted underneath code that never
moved.

## Three suspects, none guilty alone

It took my team a while to accept the shape of this bug, because it doesn't
have a single cause. It has three. Each one, on its own, was completely fine.
They had coexisted happily for a long time. The crash only appeared when all
three lined
up at once — and the day they lined up, nobody on the team had done anything to
make it happen.

Here are the three suspects.

## Suspect one: AWS quietly updated the runtime

The function runs on the managed .NET 8 Lambda runtime. AWS owns that runtime,
patches it, and rolls out new builds on its own schedule. At some point it moved
to a newer build (`dotnet:8.v88`).

That newer runtime ships its own AWS bootstrap library — the glue that sits
between Lambda's execution environment and your handler. And the new bootstrap
was built against a newer `Amazon.Lambda.Core`, one that introduces a brand-new
type: `ILambdaResponseStream`.

This is normal. Runtimes get updated. New types get added. Nobody asked us, and
nobody needed to. From AWS's side, this was an ordinary improvement.

## Suspect two: our bundled library was older

Our function still bundles `Amazon.Lambda.Core 2.8.1`. That version does not
contain `ILambdaResponseStream`. My team confirmed it the tedious way — by
inspecting every installed version of the library up to 2.8.1. None of them have
the type.

So now there are two copies of the same AWS library in play: the newer one AWS
brought with its updated runtime, and the older one we packaged ourselves. They
disagree about which types exist.

On its own, this is still harmless. A version skew like this sits dormant all
the time. Two libraries can hold slightly different views of the world and
never collide — right up until something forces them to be reconciled. Nothing
in normal operation reads *every* type in *every* loaded assembly.

Until something does.

## Suspect three: the upgrade that made everything strict

The third suspect is the only thing that actually changed on our side, and it
looked completely innocent: a routine dependency-upgrade PR that bumped
AutoMapper (and, alongside it, MediatR).

Both of those libraries work by scanning assemblies at startup to discover what
they need — AutoMapper looks for mapping profiles, MediatR looks for handlers.
And the way we'd wired them up, we asked them to scan **every loaded assembly**.
That's a common pattern, and it had worked for years.

But "every loaded assembly" includes AWS's runtime bootstrap library. When the
upgraded AutoMapper walked that library and tried to enumerate its types, it hit
the reference to `ILambdaResponseStream` — a type that lived in the newer
`Amazon.Lambda.Core` but not in the 2.8.1 we'd bundled. The reference couldn't
be resolved, the type load blew up, and because this happened during startup
scanning, it took the entire function down with it.

The detail that makes this maddening: before the upgrade, the scan tolerated
this. The older scanning behavior shrugged at a type it couldn't fully resolve.
The new version is stricter. Same instruction from us — "scan everything" — but
now "everything" was enforced to the letter.

So that's the full collision. A **new AWS runtime** brought a library with a new
type. Our **old bundled library** lacked that type. And a **newly strict scan**
insisted on reading every type in every assembly, including AWS's. Remove any
one of the three and there's no crash. Put them together and startup dies.

## The fix

Once the cause is clear, the fix is almost boring — which is exactly what you
want from a root-cause fix.

AutoMapper and MediatR never had any reason to inspect AWS's internal runtime
libraries. There are no mapping profiles of ours in there. There are no handlers
of ours in there. We were asking two of our libraries to rummage through
infrastructure we don't own, looking for things that could only ever live in
code we wrote.

So we stopped doing that. Instead of scanning every loaded assembly, we scan
only our own:

```csharp
// Before — scans EVERY loaded assembly, including AWS's runtime libraries
services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());
services.AddMediatR(cfg => cfg.RegisterServicesFromAssemblies(
    AppDomain.CurrentDomain.GetAssemblies()));

// After — scan only our own assemblies
var ourAssemblies = AppDomain.CurrentDomain.GetAssemblies()
    .Where(a => a.GetName().Name?.StartsWith("YourApp.") == true)
    .ToArray();

services.AddAutoMapper(ourAssemblies);
services.AddMediatR(cfg => cfg.RegisterServicesFromAssemblies(ourAssemblies));
```

(That's illustrative — your filter is whatever prefix your own assemblies share
— but the shape is the point.)

No functional behavior changes. The mappings and handlers that mattered all live
in our assemblies, so narrowing the scan finds exactly the same set of them. The
build passes cleanly. And as a bonus, the function is now immune to this entire
class of problem: AWS can update its runtime, swap its bundled libraries, and
add as many new types as it likes, and our startup scan will never look at any
of it.

## The lesson

The narrow, technical takeaway is simple: **scan only what you own.** When a
library discovers your types by reflection, point it at your code, not at the
whole process. Reaching into assemblies you don't control to find your own
mappings is asking to be surprised by someone else's release notes.

The broader lesson is the one I keep relearning. Dangerous production bugs are
usually combinations, not single causes. Each ingredient here passed its own
review. The AWS runtime update was correct. Our bundled library version was
fine. The dependency upgrade was a clean, sensible bump. There was no bad commit
to find, because the bug didn't live in any one change — it lived in the
intersection of three.

And "nothing changed" is almost never true. Our code didn't change, but the
environment it runs in did, and a managed runtime is part of your dependency
graph whether you think about it that way or not. Latent version skew is sitting
in most systems right now, invisible, waiting for something to force every type
to be enumerated. The upgrade that finally did the forcing got the blame, but it
was only the third domino.

The fix took just minutes. Understanding why three innocent things added up to
a crash took longer — and was the part actually worth writing down.

— Roger
