---
title: "The Patterns Didn't Go Away. You Stopped Asking for Them."
comments: true
tags:
  - AI
  - Software Engineering
  - Code Quality
  - Engineering Leadership
  - Practices
date: 2026-06-22 00:00:00.000000000 -05:00
excerpt: >-
  Two posts crossed my feed the same week — one a 248,000-PR study, one a
  reflection on how we used to build — and they told the same story from
  opposite ends: AI didn't lower the bar on code quality. We stopped holding it
  there. The discipline still works. You just have to ask for it.
header:
  teaser: images/fotis-fotopoulos-DuHKoV44prg-unsplash.jpg
  overlay_image: images/fotis-fotopoulos-DuHKoV44prg-unsplash.jpg
  overlay_filter: 0.5
  caption: "Photo by [**Fotis Fotopoulos**](https://unsplash.com/@ffstop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [**Unsplash**](https://unsplash.com/photos/DuHKoV44prg?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)"
categories:
  - Technology
  - Development
---

Two posts crossed my feed the same week, from people who don't know each other,
making what looked like opposite arguments. They were actually making the same
one.

The first was a study. Stephen Poletto's team at Span looked at **248,099 pull
requests and 65,697 production incidents** and went hunting for the headline
everyone expects by now: *does AI write buggier code?* They couldn't find it.
AI authorship, on its own, wasn't a statistically significant driver of defect
rate. The teams shipping AI-assisted code cleanly and the teams shipping it into
a dumpster fire had the *same* AI. What separated them was everything around the
AI — review discipline, ownership boundaries, how much room they left for
refactoring, whether anyone capped the size of a pull request.

The second was a reflection. Jamie Sharp wrote about learning to build software
in the early 2000s, when "design was the work" and "the code was an artifact" —
when engineers shared a vocabulary of patterns and watched complexity on
purpose. His worry about now isn't that the tools got worse. It's that we
quietly decided the standard was optional: ask an agent to "build the thing,"
accept whatever comes back, ship it. No spec, no design, no bar the output has
to clear. His line stuck with me: *the tools didn't lower the bar — we did, by
deciding the bar was optional.*

One post is data. One is memory. They point at the same conclusion. The quality
problem people blame on AI isn't coming from the AI.

## The patterns didn't go anywhere

Here's the part that should be reassuring and is mostly just inconvenient: every
practice that made code good before still makes code good now. Single
responsibility. Clear boundaries. Dependencies pointing the right direction.
Small, reviewable changes. Tests that double as design feedback. None of that
got repealed. Span's findings are basically a measurement of those practices —
the teams with PR discipline and real ownership are the ones AI made *faster*,
not messier.

What changed is that the patterns stopped being automatic. For twenty years they
rode along inside the act of typing. You couldn't write a class without deciding
what it was responsible for, because you had to write every line of it. The
friction did some of the thinking for you. Generation removed the friction, and
it took the accidental discipline with it. The patterns are still sitting right
there. They're just no longer free.

## AI is a junior dev who never internalizes anything

The mental model I keep coming back to: an AI agent is the most capable junior
developer you will ever work with, and also the one who will never, on its own,
develop judgment.

A good junior gets a vague ticket, takes a swing, and hands you something that
works and is shaped wrong. You don't conclude the junior is hopeless. You tell
them: this method's doing three things, split it; this reaches into another
module's internals, pass it in; this needs a test, and if the test is hard to
write, the design is the problem, not the test. Say it enough times and a human
junior starts doing it before you ask. That's what "getting more senior" *is* —
internalizing the standard so it stops needing to be said.

The agent never makes that move. It will apply every pattern you name, cleanly
and instantly, and forget to apply a single one you didn't. It has no standard
of its own to fall back on. Which means the standard has to come from you, every
time, out loud. The teams getting great results aren't using better models.
They're the ones still doing the senior half of the job — naming the patterns
the agent should follow, the way they'd direct a junior who hasn't learned them
yet.

## Garbage in, garbage out — now at full speed

"Ship the thing" is a garbage prompt, and it produces exactly what it asks for:
code with no spec to satisfy, no design to honor, no bar to clear. It compiles.
It might even pass tests. And, in Sharp's words, nobody — human or agent — can
safely change it later, because there was never a design to change. That's not
an AI failure. Feed that brief to a contractor and you'd get the same slop, just
slower.

Flip the inputs and the output flips with it. Tell the agent the responsibility
each piece owns. Point it at the seam you actually want. Hand it the constraints
a good reviewer would enforce anyway. Cap the change so the review surface stays
human-sized — Span singled this out, because the one thing AI reliably *does*
inflate is PR size, and a giant diff is where review quietly stops happening.
Same model, same afternoon, completely different code. Garbage in, garbage out is
not a new law. AI just removed the wait between the garbage going in and coming
back out, which makes the quality of your inputs the whole game.

## The bar is a choice you make on purpose now

I've [written before](/2025/09/building-with-ai/) about treating AI like a pair
who types at 300 words a minute, not a lead architect — letting it draft, then
spending ten minutes on responsibilities, boundaries, and names before anything
merges. That checklist matters more now, not less, because the thing it's really
defending is the bar itself. The discipline used to be enforced by how slow
writing code was. It now has to be enforced by you, deliberately, against a tool
whose entire appeal is that it removed the slowness that used to enforce it.

That's the uncomfortable shift hiding inside both posts. The standard didn't
move and the patterns didn't expire. They just lost their free ride. Holding the
line on code quality is no longer something that happens to you while you work —
it's a decision you make, out loud, on every change, or it doesn't happen at all.

So the question Sharp leaves you with is the right one to sit with: are you using
these tools to ship faster, or to skip the part of the job that was always the
actual job? The good news, and the Span data backs this up, is that the teams who
kept doing the actual job are the ones pulling ahead. The patterns work. They
always did. You just have to ask.

— Roger

## Further reading

- Poletto, Stephen.
  ["We looked at 248,099 PRs and 65,697 production incidents."](https://www.linkedin.com/posts/spoletto_we-looked-at-248099-prs-and-65697-production-share-7467946179687763968-a0Jb/)
  — the Span study finding that AI authorship isn't the defect driver; the
  engineering environment around it is.
- Sharp, Jamie.
  ["When I learned to build software in the early 2000s…"](https://www.linkedin.com/posts/jamie-sharp-mba-b8247911_when-i-learned-to-build-software-in-the-early-activity-7471747440220565504-Bhd4)
  — on design as the real work, and the bar we decided was optional.
