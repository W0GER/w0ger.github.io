---
title: "Building with AI Without Drowning in Technical Debt"
comments: true
tags:
  - AI
  - Software Engineering
  - Technical Debt
  - Architecture
  - Practices
date: 2025-09-18 00:00:00.000000000 -05:00
excerpt: >-
  AI makes it fast to ship—but just as fast to harden bad design. Here’s a
  practical approach I use to keep speed without compounding debt.
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

If you’ve built anything meaningful with AI at your side, you’ve probably felt
the rush: prompts fly, code appears, tests turn green, dopamine hits. Then
reality shows up—small changes start touching too many files, abstractions
multiply, and what felt like momentum becomes molasses. I’ve seen this across
teams and my own projects. The speed is real. So is the debt.

Andrew Stellman captured this dynamic well in his piece on AI-resistant
technical debt: "vibe coding"—rapid prompt → generate → run → paste errors →
regenerate—can turn exploration into accidental architecture if we don’t check
it. The result is familiar: over-coupling, god objects, needless layers, and
eventually shotgun surgery for simple changes. The trap isn’t that AI is wrong.
It’s that AI is convincing. It compiles, it passes tests, it feels done. But
design debt accrues silently. See the original commentary here:
[Building AI-Resistant Technical Debt](https://www.oreilly.com/radar/building-ai-resistant-technical-debt/).

## My stance

AI is a great accelerator for working software. It is a terrible decider of
design. I treat it like a pair who can type at 300 WPM, not a lead architect.
That mindset shift keeps me fast without locking bad decisions into the
foundation.

## The failure modes I watch for

- Over-engineered indirection for simple I/O
- Hidden coupling (helper classes reaching into internals)
- Abstractions created to satisfy tests instead of improving design
- Test pain as an early warning system
  (if adding a test feels hard, the design is hard)

## Guardrails that actually work in practice

1. Trust, then verify (quickly)

   Let AI draft. Then I do a 5–10 minute design pass: responsibilities,
   boundaries, and names. If I can’t describe each unit’s single responsibility
   in one sentence, I refactor before merging.

1. Prefer simpler seams over frameworks

   Instead of wrapping I/O in a mini-architecture, pass inputs as parameters and
   return values. Push complexity to the edges only when genuinely needed.

1. Tests as design feedback, not just safety nets

   When a test is hard to write, I stop and adjust the API or dependency
   direction. Pain here is a feature; it points to structure that wants to change.

1. Time-boxed exploration, deliberate consolidation

   I allow messy exploratory branches. But I always follow with a consolidation
   commit: rename for clarity, inline accidental abstractions, extract true seams,
   delete dead code.

1. Naming is a design act

   I take an explicit naming pass. Clear names reduce the surface area of
   confusion more than another layer of code ever will.

## A lightweight working checklist

Use this when accepting AI-generated code:

- Single responsibility per module or class?
- Dependencies point inward (domain) vs. outward (frameworks)?
- Input/Output handled at edges, not sprinkled through core logic?
- Tests easy to write without elaborate scaffolding?
- One level of abstraction per function? If not, split.
- Names read like documentation? If not, rewrite.

## Patterns I reach for instead of over-architecture

- Data-in, result-out functions for core logic
- Ports-and-adapters only where boundaries are real (DB, network, UI)
- Composition over inheritance
- Feature flags and strangler patterns for incremental change

## Team habits that prevent AI-accelerated debt

- Short design reviews for AI-heavy PRs (10 minutes, 3 questions:
  responsibilities, coupling, testability)
- "Consolidation Fridays"—dedicated time to rename, simplify, and pay back
  tiny debts before they grow
- Metrics that reward clarity (diff readability, test friction reduced) not
  just throughput

## Final thought

AI makes starting easy and finishing tempting. Craft lives in the middle—where
we decide what stays, what goes, and what gets clearer. Move fast, but edit
harder.

If this topic resonates, the O’Reilly piece is a solid read:
[Building AI-Resistant Technical Debt](https://www.oreilly.com/radar/building-ai-resistant-technical-debt/).
And if you try the checklist above, I’d love to hear what changed in your code
reviews.

— Roger
