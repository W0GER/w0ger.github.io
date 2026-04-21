---
title: "Your Backlog Is a Conversation. Your AI Agents Need a Contract."
comments: true
tags:
  - AI
  - Agile
  - Software Engineering
  - Backlog
  - Product Management
date: 2026-04-21 00:00:00.000000000 -05:00
excerpt: >-
  User stories assume humans will fill in the gaps. Autonomous agents don't.
  Here's how to turn tickets into machine-ready contracts — and why the backlog
  is becoming the real interface between intent and execution.
header:
  teaser: images/getty-images-iLLoCMbfpPc-unsplash.jpg
  overlay_image: images/getty-images-iLLoCMbfpPc-unsplash.jpg
  overlay_filter: 0.5
  caption: >-
    Photo by [**Getty Images**](https://unsplash.com/@gettyimages)
    on [**Unsplash**](https://unsplash.com/photos/human-and-robot-handshake-hands-close-up-blurry-human-mechanical-assistant-tactile-sensitivity-artificial-intelligence-iLLoCMbfpPc)
categories:
  - Technology
  - Development
---

Last month I watched an autonomous coding agent pick up a ticket that read, in
full: *"As a customer, I want saved searches so I can return to my favorite
filters later."* Thirty minutes later it had cheerfully rewritten the session
middleware, invented a new database table, and opened a pull request with a
confident title and a test suite that passed against the code it had just made
up.

It was, technically, a working implementation. It was also completely wrong.

The ticket wasn't bad. A human engineer on the team would have glanced at it,
walked to the next desk (or opened a Slack DM), confirmed three unspoken
assumptions, and shipped something reasonable by lunch. The story assumed a
conversation. The agent didn't have one.

This is the problem that catches most teams off guard when they bring AI agents
into real delivery work. The backlog we've spent fifteen years refining is a
beautifully human artifact. It rewards empathy, tolerates ambiguity, and leaves
space for tacit knowledge. Drop an autonomous agent into the middle of that same
pipeline and every helpful ambiguity turns into a failure mode.

## The hidden contract of a user story

A well-written user story is less a specification than an invitation. *"As a
user, I want..."* is a prompt for a conversation between the developer, the
product owner, and whatever stakeholder is about to be inconvenienced by an
ill-considered implementation. The story carries maybe twenty percent of the
information; the other eighty lives in the heads of the people working on it.

Humans are exceptional at reading that eighty percent from context. We know
which module owns the authentication path. We've been burned before by the ORM's
quirks. We remember that the CTO has Strong Opinions about rate limiting. Agents
know none of this. They have a context window and whatever you put in it.

So the first shift is an uncomfortable one: for work an agent will pick up, the
ticket has to stop being a conversation starter and start being an actual
contract.

## What a machine-ready ticket looks like

The tickets I've seen work best for agents share a few structural traits.

**A concrete interface.** Not <em>"the API should return the user's saved
searches"</em> but the exact request and response shapes, field names and types
included. If it's a database change, the table and column. If it's a UI change,
the component file and the props it accepts. The agent cannot ask what you mean.

**An explicit blast radius.** A short list of files or modules the agent is
allowed to modify, and — more importantly — a list of ones it must not touch.
Without this, agents have a habit of "improving" things while they're in the
neighborhood. Last week I saw one refactor an entire logging utility because it
thought it could be cleaner. It could be. That wasn't the ticket.

**The context, inline.** If the work depends on a specific doc, the relevant
section goes in the ticket. If it depends on a library version, the version goes
in the ticket. The agent won't wander off to Confluence to check. Whatever's not
in the context window might as well not exist.

**Acceptance in executable form.** Tests, cURL commands, or a short script that
can be run to verify the change. Pass/fail is the kind of signal agents can
actually work with. "Looks good to me" is not.

None of this is especially novel — a rigorous human engineer would welcome the
same artifact. The difference is that for humans it's a nice-to-have, and for
agents it's the difference between shipping and an expensive PR full of
confident nonsense.

## Refinement, with a machine in the loop

Backlog refinement has always been the place where tickets get sharp enough to
work on. The interesting move some teams are making is putting a model in that
loop *before* the humans get there.

The pattern is simple: a cheap model reads every new ticket and flags the ones
that are missing the things agents need — no schema, no explicit scope, no
verifiable acceptance criteria. It doesn't write the ticket. It just refuses to
let a fuzzy one through the gate, with a note like <em>"no defined response
schema; an agent cannot execute this safely."</em>

This catches problems that would otherwise surface as a failed agent run three
days later. And, almost as a side effect, it tends to make the tickets better
for the humans too. Turns out precision scales.

## Estimation, when the worker bills per token

Story points were always a proxy — a way to talk about complexity and risk
without pretending we could predict wall-clock time. They work because humans
share a rough intuition for what "a 3" feels like.

Agents don't have that intuition, and their costs are structured completely
differently. A ticket that would take a senior engineer an hour might cost ten
cents or ten dollars for an agent to run, depending almost entirely on how much
context has to be loaded and how many tool calls are needed to converge on an
answer.

Teams running hybrid workflows are starting to estimate two things on a ticket:
the human complexity (still useful, still fuzzy) and the agent cost envelope, in
tokens or dollars or compute minutes. The second number unlocks a call that
didn't exist before — is this ticket worth $30 of agent time, or is it better
handled by a human while the bot works on something higher-leverage? That
tradeoff is a real one now, and it belongs on the ticket.

## Pinning the strategy to the agent itself

Here is the trickiest part. A good human engineer carries the product's strategy
around in their head. They won't build the feature the right way if they don't
know what "the right way" means for *this* product, this quarter, this company.
That intuition shapes a thousand small decisions that never show up in a ticket.

Agents start every task fresh. Unless you put the strategy into their context,
they don't have one.

The teams doing this well are treating the product direction — the current
quarter's goal, the architectural guardrails, the non-negotiables — as something
they inject into every agent prompt via retrieval. Not as a slogan pinned above
the coffee machine, but as literal text the model sees before it writes a single
line of code. *"This quarter we're optimizing for latency over throughput"*
stops being a Notion page and starts being a constraint the model is measured
against on every pull request.

When you do this, the strategy stops being decorative. It becomes load-bearing.

## The backlog is the interface

The throughline in all of this is that the backlog has quietly changed jobs. It
used to be a shared to-do list. Now, for any team with agents in the mix, it's
the primary interface between human intent and machine execution. It's where
ambiguity is either resolved or becomes a bug. It's where strategy either shows
up in the work or doesn't.

That's not a small shift, and I suspect most teams will make it by accident, one
painful PR at a time. The ones that make it deliberately — treating tickets as
contracts, refinement as a pipeline with both human and machine gates,
estimation as a real cost question, and strategy as something the agents can
actually see — are the ones who'll get real leverage from autonomous tools
instead of just faster ways to generate confident nonsense.

The backlog was always supposed to be the source of truth. It just has to earn
the title now.
