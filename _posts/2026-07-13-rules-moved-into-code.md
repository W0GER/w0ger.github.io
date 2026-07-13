---
title: "The Rules Moved Into Code. Did the Humans Come Along?"
comments: true
tags:
  - AI
  - Engineering Leadership
  - Product Management
  - Change Management
  - Review
date: 2026-07-13 00:00:00.000000000 -05:00
excerpt: >-
  Nate B Jones says your roadmap is why you're losing to AI-native teams, and
  his fix is to move the org's implicit rules into working code — fifteen
  commandments' worth. A review of the video: what lands, what rhymes with
  things I've been arguing here, and the one instruction I'd push back on.
header:
  teaser: images/john-matychuk-Af8ZjGMsHKQ-unsplash.jpg
  overlay_image: images/john-matychuk-Af8ZjGMsHKQ-unsplash.jpg
  overlay_filter: 0.5
  caption: >-
    Photo by [**John Matychuk**](https://unsplash.com/@john_matychuk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [**Unsplash**](https://unsplash.com/photos/books-and-pencil-on-map-Af8ZjGMsHKQ?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
categories:
  - Technology
  - Development
---

The title is bait, and I took it. Nate B Jones — whose *AI News & Strategy
Daily* channel is one of the more consistently substantive things in my feed —
put out a video called
["Your Roadmap Is Why You're Losing to AI-Native Teams"](https://www.youtube.com/watch?v=hYcOFTMesGc),
and I went in braced for another *Agile is dead* eulogy. That's not what this
is. It's something more useful, and in a couple of places it's making an
argument I want to have out loud.

His setup will sound familiar if you've read this blog lately: AI made it
cheap to build almost anything, and most companies still ship at the old pace.
The reason, he argues, isn't that their models are worse than Anthropic's or
OpenAI's. It's what they have — or haven't — moved out of meetings and
documents and into working code.

## The argument in one move

Jones's core claim is that every organization runs on implicit rules. They
live in meeting cadences, approval chains, templates, and the tone of voice
someone uses when they say *that's not how we do it here*. Those rules weren't
arbitrary — they were sensible responses to scarcity. Engineering time was
expensive. Context was slow to share. Mistakes were costly. The conditions
argued for the rules.

Then AI dissolved the scarcity, and the rules kept enforcing themselves out of
pure inertia. His fix is blunt: an operator's job now includes rewriting the
implicit rules as explicit, machine-readable ones — and then moving the
repeatable coordination they govern into code. Not a values poster.
Constraints that run: calendar checks, Slack challenges, audit tools, hard
blocks. He wrote fifteen "commandments" for his own operation and walks
through them in clusters. An **engineering-and-product cluster**: don't slow
engineering down; product makes no roadmaps and doesn't direct engineering
time — instead it's in the terminal daily, sitting with engineering and
jamming. A **design-and-documentation cluster**: no meetings over an hour;
documentation as code; design moves into the code, the SDK, and the UI. And
a **human cluster**: stay flexible enough to deliver value like water over
stone; build with a team; help along the folks who aren't going as fast, and
learn from the ones who are.

The line that stuck with me is from the companion essay: a rule that lives
only in the head of your longest-tenured director does not exist, as far as
your stack is concerned. That's the legibility problem in one sentence. Your
agents can't follow a rule nobody wrote down, and increasingly, neither can
your people.

## Where it lands

This rhymes hard with things I've been circling here for months, which is
probably why I liked it.

I argued in
[The Patterns Didn't Go Away](/2026/06/patterns-didnt-go-away/) that the
quality bar didn't move — it just lost its free ride, and now it has to be
stated out loud on every change. Jones takes that a step further than I did:
don't just say the standard out loud, encode it where the work happens, so it
gets enforced without a senior person spending judgment on it every time. And
when I wrote about
[turning backlog items into contracts for AI agents](/2026/04/backlog-contract-for-ai-agents/),
I was making his argument at the scale of a single ticket. He's making it at
the scale of the whole operating system.

The sharpest tool in the video is what he calls the enforcement ladder: a rule
can be a value, an instruction, a reminder, a hard block, or a decision
explicitly owned by a human — and you choose the rung deliberately. Most
organizations I've seen only have the two ends: aspirational values nobody
checks, and escalations to a person. The three middle rungs are where the
leverage is, and they're exactly the rungs that AI made cheap to build. His
example of an audit tool that enforces the *kill monthly meetings*
commandment is the whole thesis in miniature — coordination that used to cost
a recurring hour of ten people's attention, replaced by a check that runs.

Even the bait holds up. "Kill the roadmap" turns out to mean roughly what I
meant by opportunity backlogs over feature backlogs: when building is cheap, a
committed list of outputs is a liability, and the roadmap's real functions —
alignment, sequencing, saying no — get absorbed by the other rules. He's
explicit that the prohibition only works because the rest of the system picks
up the load. Which brings me to the part where I got off the bus.

## Where I push back

Jones insists the fifteen commandments work as one system, and that partial
adoption is where this fails — you can't cherry-pick the rule that feels
easiest. His example is the org that stops holding roadmap meetings but never
gets product into the terminal: the coordination is gone, the replacement
never got installed, and what's left is chaos wearing an AI-native costume.
As a description of the *design*, he's right, and he's honest about it in a
way most playbook-sellers aren't. He even warns that copying somebody else's
constitution is how you end up with a document that enforces nothing.

But "every rule has to move together" is a big-bang change program, and I just
spent a whole post arguing that
[organizations have a speed limit](/2026/06/org-speed-limit/) on absorbing
exactly this kind of change. Fifteen simultaneous rewrites of how people
meet, document, design, and decide is a lot of Everett Rogers' adoption curve
to swallow in one gulp — and pushing past that limit doesn't accelerate
adoption, it manufactures resistance. The failure mode he's worried about (cherry-picking)
and the failure mode I'm worried about (rejection of the transplant) are both
real. The way through isn't all-at-once; it's sequencing the rules so each
one, once absorbed, makes the next one cheaper to adopt — and being honest
that the interlocking design means you haven't captured the full value until
the set is in. That's a harder message than *move it all together*, but it's
the one that survives contact with an actual org chart.

## The takeaway worth stealing

Don't steal the commandments. Steal the method. For any rule your org
enforces by habit: name the behavior, find the scarcity that originally
justified it, ask whether that scarcity still exists, and if it doesn't,
rewrite the rule as a testable constraint and pick its rung on the ladder.
That exercise costs you an afternoon, and it's the part of the video I expect
to still be using a year from now.

The photography analogy Jones opens with is the right frame to leave on: when
taking a picture became free, photography didn't die — judgment about which
picture to take became the entire job. Building is going the same way. His
bet is that the judgment belongs in code, where it compounds. Mine is that it
gets there at the speed your people can absorb it, and not one commandment
faster. Both things can be true. Watch the video and argue with us.

— Roger

## Further reading

- Jones, Nate B.
  ["Your Roadmap Is Why You're Losing to AI-Native Teams."](https://www.youtube.com/watch?v=hYcOFTMesGc)
  *AI News & Strategy Daily*, YouTube — the video under review.
- Jones, Nate B.
  ["AI-Native Companies Run on Code."](https://natesnewsletter.substack.com/p/ai-native-company-rules)
  *Nate's Newsletter*, Substack — the companion guide, with the full ruleset,
  the enforcement ladder, and the five-question worksheet.
