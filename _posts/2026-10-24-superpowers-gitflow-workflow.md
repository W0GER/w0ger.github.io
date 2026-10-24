---
title: "My Superpowers Workflow, GitFlow Edition"
comments: true
tags:
  - AI
  - Claude Code
  - Software Engineering
  - Git
date: 2026-10-24 00:00:00.000000000 -05:00
excerpt: >-
  Andrew Connell wrote up the loop he used to run a 415-issue project with
  Claude Code and superpowers. Mine is nearly the same, but it ships a
  real iOS game through GitFlow instead of release-please. Here's the loop,
  where it differs, and how to start.
header:
  teaser: images/lois-hill-3pWCaJfy2HA-unsplash.jpg
  overlay_image: images/lois-hill-3pWCaJfy2HA-unsplash.jpg
  overlay_filter: 0.3
  caption: >-
    Photo by [**Lois Hill**](https://unsplash.com/@loishillphotography?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
    on [**Unsplash**](https://unsplash.com/photos/3pWCaJfy2HA?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)
categories:
  - Technology
  - Development
---

Andrew Connell just published
["How I ran a 415-issue project with Claude Code and superpowers"](https://www.andrewconnell.com/articles/superpowers-workflow-415-issue-program/),
and reading it was a little eerie. It's very nearly my process, step for
step, written up more carefully than I'd ever have bothered to. If you
only read one post about
running real work through an AI agent, read his. It has the full example
issue, spec, plan, and ADR inline, and it's the better reference.

This post is the version for my setup. Same loop, two real differences, and
a shipping app to show it on. I'm writing it for the people I keep talking
to who are *vibe coding*: getting real things built with an AI agent, but
improvising every session. It works right up until it doesn't, and the
moment it stops working is usually the moment you realize nobody — not you,
not the agent — remembers why the code is the way it is.

The fix isn't a better prompt. It's a loop you run the same way every time.

## The project

The proof here is [Lamplit](/2026/03/lamplit/), the daily acrostic puzzle
game my company Alpine Blue ships for iPhone and iPad. It's a SwiftUI app
with in-app purchases, Game Center, CI/CD to TestFlight, and a content
calendar that needs a new puzzle every single day.

Since the repo was created on February 25, 2026, it has run through about
135 issues, 147 merged pull requests into `develop`, and 13 releases to
`main`, from v0.3 to v1.3.0, which shipped this week with native iPad and
iPhone Duo layouts. That's one person and an agent. Andrew's numbers are
bigger — 415 issues, 157 specs, 140 ADRs — and you should weigh mine
accordingly. But the shape holds at both sizes, which is the point.

## The loop

Andrew describes seven steps. I run the same seven. Here's each one, with
where I differ.

### 1. Every change starts as an issue

No issue, no work. That's a standing rule the agent knows, not a habit I
try to remember. I describe what I want in a sentence or two, and the agent
drafts a GitHub issue that works as a lightweight PRD: a user story, the
context, and acceptance criteria written as checkboxes.

Here's the top of a real one, the iCloud sync feature that gated the iPad
release:

```markdown
**As a** player who solves on more than one device (iPhone, iPad, iPhone Duo)
**I want** my progress, streak, hints and shields to follow me through iCloud
**So that** I can start the daily puzzle on my iPhone, finish it on my iPad,
and keep one streak
```

The acceptance criteria underneath are the contract. If you've read my post
on
[turning backlog items into contracts for AI agents](/2026/04/backlog-contract-for-ai-agents/),
this is that idea at the scale of one feature: agents don't fill gaps the
way people do, so the gaps have to be closed before the work starts.

### 2. Brainstorm, one question at a time

I run `/superpowers:brainstorming` with the issue number. The
[superpowers](https://github.com/obra/superpowers) plugin turns Claude Code
into an interviewer: it asks one question at a time and plays back what it
heard until the approach and the scope are settled. This is the step that
feels slowest and pays back the most. Most of the bad code I've gotten out
of an agent traces back to a decision I never actually made.

### 3. Specs and decisions land on the issue

This is my first real difference from Andrew, and it's an honest one.

Andrew commits a design spec to `docs/superpowers/specs/` for every
meaningful change, and records lasting decisions as ADRs. I've only just
started committing those. Lamplit has exactly one committed spec and no
ADRs yet.

What I *have* been doing all along is having the agent post its spec and
the decisions to the issue as it works. The iCloud issue has a `## Plan`
comment that opens like this:

```markdown
**Decisions (Roger, 2026-10-23):** recompute the streak from synced
dailies; keep a ledger of hint and shield grants and spends; sync is always
on when signed in to iCloud; one status line in Settings. **The iPad
release waits for this**, because an iPhone + iPad player is the common
case.
```

That puts the reasoning right next to the request, where anyone reading the
issue will find it. What it doesn't do is put the reasoning in the repo,
where the *agent* will find it next month. That's the gap Andrew's ADRs
close: they're the agent's long-term memory. So I opened an issue to
backfill specs and ADRs from those comments, and to make committing them
part of the rule going forward. If you're starting from scratch, start
where Andrew is, not where I was.

### 4. Plan, then throw the plan away

The agent turns the spec into a task-by-task implementation plan. Like
Andrew, I mostly don't review it. I review the *spec*, because that's where
intent lives. A plan is a working document; the line numbers in it start
drifting the moment the first task lands. Andrew deletes plans before they
ever reach `main`. Specs stay, plans go.

### 5. A worktree and a branch per change

Each change runs in its own git worktree on its own branch, never in my
main checkout. That's what lets me run more than one session at once
without them stepping on each other. A project board tracks where each
issue is, and a set of house rules the agent loads every session covers the
things I'd otherwise repeat: issue numbers are required, tests come first,
nothing goes straight to a protected branch.

### 6. A pull request, reviewed by a fresh agent first

Everything lands through a pull request. This is the one piece of Andrew's
loop I *wasn't* running, and I've stolen it.

Before I look at a PR, a fresh agent reviews it: a new session with none of
the context from the session that wrote the code. It doesn't share the
implementer's assumptions, so it catches the things the implementer talked
itself into. I'm using it now on the port of the
[lamplit.games](https://lamplit.games) website from a web-builder vendor to
a static site, and it's going into the game's process next sprint.

Then I review for intent, not line by line. Did it do what the issue asked?
Do the tests pass? Does the app on my phone do the right thing? If so, it
gets squash-merged, and the branch and worktree go away.

The squash title matters more than it looks. It has to be a
[Conventional Commit](https://www.conventionalcommits.org/): `feat(sync):
...`, `fix(ci): ...`, `chore(deps): ...`. A GitHub Action rejects any PR
title that isn't one, because of what happens next.

### 7. Release through GitFlow

This is the second real difference, and the biggest.

Andrew uses
[release-please](https://github.com/googleapis/release-please). Code can
land on `main` without reaching production; release-please keeps a standing
release PR open, and a release only ships when that PR merges. It's a gate
between "merged" and "shipped."

I get the same gate from
[GitFlow](https://nvie.com/posts/a-successful-git-branching-model/)
instead. Lamplit has two long-lived branches:

- **`develop` is the beta.** It's the default branch, and every feature PR
  targets it. Any branch, including `develop`, can be built and sent to
  TestFlight on demand for testing on real devices. Those builds don't get
  tagged and don't publish a release.
- **`main` is production.** A release is a PR from `develop` into `main`.
  When it merges, CI/CD builds the app, uploads it, tags the version, and
  publishes a GitHub Release. Then a merge-back PR brings `main` back into
  `develop`.

Versioning comes from [GitVersion](https://gitversion.net/) instead of
release-please. It reads the Conventional Commit squash titles on `develop`
to pick the next version: `feat` bumps the minor, `fix` and `perf` bump the
patch. That's why the PR title check exists. A title that isn't a
Conventional Commit silently loses its version bump, so it gets caught at
PR time, not release time.
[Release Drafter](https://github.com/release-drafter/release-drafter) keeps
the release notes drafted as PRs land.

The trade-off is the same one Andrew names for release-please: merging the
release PR becomes a step you can't skip. For an App Store app, that's
exactly what I want. "It's on `develop`" and "it's in players' hands" are
different states, and the `develop → main` PR is the single, deliberate
moment one becomes the other.

### And then, an ADR

When a change made a decision with a lasting trade-off, it gets an ADR, so
the next session — human or agent — doesn't relitigate it. This is the step
I'm newest at. See step 3.

## Milestones follow the product

One more small difference. Andrew uses milestones for large efforts, not
sprints. Mine follow Lamplit's content calendar.

The game needs a puzzle every day, and I build those in batches of about 90
days. So milestones line up with calendar quarters. When a quarter has more
than one release, I suffix it — *2026 Q4 Sprint 1*, *2026 Q4 Sprint 2* —
purely as buckets to group issues into. There's no ceremony attached to the
word "sprint." The cadence comes from the product, and the milestones just
make it visible.

## Who decides what

The part of Andrew's post I'd underline is where the human sits in the
loop, because it's the answer to vibe coding's real problem:

- **I decide** at the issue, the brainstorm, and the spec. That's where
  intent gets set, and it's the part an agent can't do for me.
- **The agent runs** the plan and the implementation, test-first.
- **I verify** at the PR — after a fresh agent has had the first pass — and
  I decide when a release goes from `develop` to `main`.

Vibe coding puts the human in the middle of the implementation, steering
line by line. This loop moves the human to both ends: setting intent before
the code exists, and judging the result after. The middle gets faster, and
the decisions stop disappearing.

## How to start

You don't need all of this on day one. Here's the order I'd adopt it in:

1. **Make "no issue, no work" a rule** the agent follows, with acceptance
   criteria on every issue.
2. **Brainstorm before you build.** Install superpowers and run
   `/superpowers:brainstorming` on the next issue you pick up.
3. **Write the spec down, and review it instead of the code.** Commit it to
   the repo, not just a comment thread.
4. **Throw plans away.** Keep specs, delete plans.
5. **Branch, PR, and squash with Conventional Commit titles**, and let a
   fresh agent review before you do.
6. **Put a gate between merged and shipped.** Release-please if you live on
   one branch, GitFlow's `develop → main` if you want a standing beta.
7. **Record lasting decisions as ADRs.** Start sooner than I did.

Then go read
[Andrew's post](https://www.andrewconnell.com/articles/superpowers-workflow-415-issue-program/)
for the full worked examples. Thanks to him for writing down the process so
clearly that I could finally see my own.

— Roger

## Further reading

- Connell, Andrew.
  ["How I ran a 415-issue project with Claude Code and superpowers."](https://www.andrewconnell.com/articles/superpowers-workflow-415-issue-program/)
  The original, with the full issue, spec, plan, ADR, and release PR
  examples.
- [superpowers](https://github.com/obra/superpowers), the Claude Code plugin
  behind the brainstorm, spec, and plan steps.
- Driessen, Vincent.
  ["A successful Git branching model."](https://nvie.com/posts/a-successful-git-branching-model/)
  The original GitFlow write-up.
