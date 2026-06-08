---
title: "AI Didn't Kill Agile. It Just Moved the Constraint."
comments: true
tags:
  - AI
  - Agile
  - Software Engineering
  - Leadership
  - Product Management
date: 2026-06-08 00:00:00.000000000 -05:00
excerpt: >-
  Agile was built to ration scarce engineering. AI made building cheap, so the
  bottleneck moved downstream — to whether anyone can actually absorb what we
  ship. The gates we built to protect capacity are now just drag.
header:
  teaser: images/growtika-FQ3lFA4Zi58-unsplash.jpg
  overlay_image: images/growtika-FQ3lFA4Zi58-unsplash.jpg
  overlay_filter: 0.5
  caption: >-
    Photo by [**Growtika**](https://unsplash.com/@growtika?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [**Unsplash**](https://unsplash.com/photos/a-computer-on-a-desk-FQ3lFA4Zi58?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)
categories:
  - Technology
  - Agile
---

There's a particular kind of meeting I've sat in a lot lately. A team demos
something genuinely impressive — an agent that drafts the integration, a tool
that turns a Figma frame into working components, a model wired into the support
queue. Everyone nods. Then someone asks the only question that matters: *who's
actually using it?* And the room goes quiet.

That silence is the whole story of AI and Agile right now. We got very good at
building things, very fast. We did not get any better at the part that comes
after.

A lot of people have read that silence as proof that Agile is finished — that
sprints and backlogs and refinement were scaffolding for a slow era we've now
left behind. I don't think that's right. Agile didn't die. The thing it was
quietly built to manage just stopped being the problem.

## The constraint we built Agile around

For twenty years, engineering capacity was the scarce resource. Good engineers
were expensive, hard to hire, and easy to waste. So we built an entire
discipline around protecting them.

Be honest about what the ceremonies were really for. The backlog rationed
attention. The sprint boundary kept stakeholders from re-pointing the team every
afternoon. Estimation was a polite way of saying *no, not this quarter.*
Prioritization, intake gates, the whole governance apparatus — all of it existed
to take a small, costly pool of build capacity and aim it at the highest-value
work while defending it from thrash.

That wasn't bureaucracy for its own sake. It was a sensible response to a real
constraint. When you can only build a little, deciding *what* to build is the
entire game.

## When the scarce thing stops being scarce

Now drop the price of building by an order of magnitude.

When a single engineer with the right tooling can produce in an afternoon what
used to take a team a sprint, the math underneath all those ceremonies quietly
breaks. The gate you built to protect a scarce resource doesn't protect anything
anymore — it just adds latency to a resource that's no longer scarce. Every
careful brake you installed is now drag.

This is the part teams feel before they can name it. The process that used to
feel like discipline starts to feel like wading through wet sand. People assume
they're doing Agile wrong. They're not. They're running a system tuned for
scarcity in a world that just got abundant on one specific axis.

## The bottleneck didn't vanish — it moved

Here's the trap, though. Cheap building does not mean fast value. It just moves
the jam somewhere else.

Look at almost any organization with real AI investment and you'll find the same
landscape: a pile of copilots, agents, internal tools, model integrations, three
pilots that demoed beautifully, and a quiet graveyard of prototypes nobody
folded into how the work actually gets done. The capability is sitting right
there. The absorption isn't.

The constraint moved downstream. It used to live in *can we build it?* Now it
lives in *can anyone put it to work and prove it was worth it?* That's not an
engineering question. It's an organizational one — about workflows, trust,
change, and the unglamorous labor of getting a new capability all the way into
someone's daily job.

## Agility's job just inverted

For two decades, agility pointed inward. Its instinct was to protect engineering
*from* the organization — buffer the team, hold the line, keep the demands out.

If the bottleneck is now adoption, that instinct is exactly backwards. The job
isn't to wall engineering off from the business. It's to push engineering *into*
it — out to the front lines, pointed straight at the highest-value adoption
problems, close enough to the work to see whether anything actually changed.

Same word, opposite motion. Agility used to mean *defend the scarce thing.* Now
it means *get the abundant thing into contact with reality as fast as possible.*

## What you replace the brakes with

The fear, reasonably, is that removing the brakes just gives you faster chaos.
And it would — speed pointed in no particular direction is simply waste,
accelerated. The answer isn't no brakes. It's swapping the external brakes of
scarcity for internal ones built on direction.

A few of the shifts I'd bet on:

**Goal-driven over spec-driven.** When building is cheap, a fat specification is
a liability — you've over-constrained the implementation before you've learned
anything. Give teams a sharp goal and the guardrails, and let them find the
shape. (I've argued before that for [AI agents this has to be explicit](/2026/04/backlog-contract-for-ai-agents/);
for humans, direction beats a script.)

**Opportunity backlogs over feature backlogs.** Stop listing things to build.
Start listing outcomes you're trying to move. A feature list assumes building was
the hard part. It isn't anymore.

**Value metrics over velocity.** Velocity measured how fast you converted the
scarce resource. Nobody cares now. Measure adoption, measure realized impact,
measure whether the thing you shipped last month is load-bearing in someone's
work today.

**A thin spine, thick edges.** Keep the central process light enough that
learning at the edge compounds instead of waiting on a committee. Empower teams,
hold them to outcomes, and resist the urge to re-add a gate every time something
goes sideways.

None of this is permission to abandon rigor. It's a relocation of it — from
controlling input to being honest about output.

## Which job is worth absorbing?

Two of those shifts — opportunity backlogs and goal-driven work — quietly lean on
a muscle most teams never had to build. Rationing scarce engineering, you mostly
needed to know what to build *next*. When building is nearly free, you need to
know what's worth building *at all* — and the sharpest name for that skill is
Clayton Christensen's Jobs to be Done.

The premise is relentlessly demand-side: people don't buy products, they hire
them to make progress in a particular circumstance. Nobody wants a quarter-inch
drill; they want a quarter-inch hole, and really they want the shelf up before
the in-laws arrive. When building was the expensive part, you could start from
the drill and survive. When building is free, the only scarce thing left is
knowing which job is worth doing — and whether your shiny new capability is a
better hire than whatever the person is using today, switching costs included.

It's also the cleanest explanation I've found for the prototype graveyard.
Christensen frames every switch as a tug-of-war: the *pull* of the new thing
against two forces of inertia — the anxiety of trying it and the habit of what's
already there. Most dead pilots had plenty of pull and made no accounting for the
inertia. The job was never really hired, so the capability never got absorbed.

I'd be honest about the limit, though. Jobs to be Done is a targeting system, not
a throughput one. It tells you which job to aim abundant capability at; it does
nothing on its own to raise how much change an organization can stomach in a
quarter. That ceiling is a different problem, and pretending one framework solves
both is how you get a tidy theory and the same graveyard. Where it pays off twice
is measurement: Tony Ulwick's outcome-driven spin turns a job into the
*measurable* outcomes people judge progress by — a far better source for those
value metrics than velocity ever was, and the same instinct as writing acceptance
you can actually run. Define done as the job getting done.

## Forward-deployed, because the value is at the edge

The pattern that keeps proving itself here is forward-deployed engineering:
putting engineers right at the point where the capability meets a real user, a
real workflow, a real customer. It's an old idea. It's newly essential, because
the gap that matters now is the one between *built* and *used*, and that gap is
only visible from the edge.

You cannot close an adoption gap from the center of the org chart. You close it
by standing next to the person who's supposed to be getting value and watching
where it falls apart.

## The real work now

I don't think the teams that win the next few years will be the ones that build
the most. Building is becoming table stakes. The ones that win will have built
something harder to copy: a system for continuously absorbing new capability into
evolving human work — and the honesty to keep asking *who's actually using it*
until the room stops going quiet.

Agile was always about responding to change over following a plan. The change
showed up. It just landed one step downstream of where we were looking.

---

*This post was sparked by Scrum.org's
[AI Didn't Kill Agile. It Moved the Bottleneck](https://www.scrum.org/resources/blog/ai-didnt-kill-agile-it-moved-bottleneck)
— worth reading in full. The argument here is my own take on the same idea.*
