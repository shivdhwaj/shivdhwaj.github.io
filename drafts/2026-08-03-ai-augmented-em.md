---
title: "The EM Job Didn't Get Smaller. It Got Rewired."
date: 2026-08-03
tags: [engineering-management, ai-tools, claude-code, team-velocity]
draft: true
---

Six months ago, my calendar told the truth about my job: a third of it was
meetings, a third was Slack triage, and a third was context-switching
between four repos trying to remember which PR was blocked on what. The
actual engineering-management work — coaching, roadmap thinking, removing
blockers that need a human's judgment — got whatever was left over, usually
late at night.

The thing that changed wasn't a new process or a reorg. It was treating
agent tooling — Claude Code, MCP-connected tools, orchestrated subagents —
as infrastructure for the EM role itself, not just something I pointed
engineers toward.

## The toil was never the hard part

Most EM toil is pattern-matching work wearing a management costume. Is this
PR blocked on a real design question or a missing test? Is this CI failure
a flaky integration test or a real regression? Does this bug report need a
senior engineer or is it a one-line fix that's been sitting for three days
because nobody owns triage?

None of that requires judgment I'm uniquely positioned to provide. It
requires attention — the scarce resource an EM actually runs out of. So I
started delegating the pattern-matching layer to agents and kept the
judgment layer for myself.

Concretely, that looks like:

- **PR and CI babysitting as a background process.** Instead of manually
  refreshing pull requests to see if CI went red, I have agents watch PR
  activity, diagnose failures, and either push a fix or flag exactly why
  they didn't. I only get pulled in when something is genuinely ambiguous
  — a merge conflict that touches shared logic on both sides, a review
  comment that changes scope. Everything mechanical resolves without me in
  the loop.
- **Multi-agent sweeps instead of solo digging.** When I need to understand
  "what's actually blocking this release," a single pass through Slack and
  GitHub misses things. Fanning that question out — one agent reading CI
  history, one reading open threads, one checking dependency PRs — and
  synthesizing the result takes minutes instead of the twenty-minute
  archaeology dig I used to do by hand.
- **MCP tooling as the connective tissue.** The value isn't any single
  integration — it's that GitHub, Slack, and internal docs are reachable
  from the same agentic loop, so "check if this got resolved" doesn't mean
  four browser tabs and a mental model of where the answer probably lives.

## What this actually bought back

The honest version of the win isn't "AI replaced my toil." It's narrower
and more useful than that: the toil got fast enough that it stopped being
the thing my day organized itself around. Standups aren't preceded by a
frantic PR-status scramble. 1:1s don't get bumped because CI caught fire.
The backlog of "I should really look into why that test is flaky" stopped
being a backlog, because an agent looks into it the day it happens instead
of the week I finally have a free afternoon.

That freed-up attention went to the parts of the job that were always the
actual job: giving an engineer direct, specific feedback instead of a vague
"good work"; noticing a junior engineer is stuck before they ask for help;
spending real time on what the team should build next quarter instead of
whether this quarter's tickets are moving.

## The failure mode to watch for

The risk with this shift isn't that the agents get something wrong — it's
that delegating the mechanical layer makes it tempting to delegate the
judgment layer too. Code review comments that require understanding *why*
a design choice matters, performance conversations, decisions about who's
ready for more scope — those don't compress well, and trying to compress
them produces management that feels automated to the people on the
receiving end. The agents are good at "did CI pass, why not, fix it." They
are not a substitute for knowing your engineers well enough to tell when
someone's quiet in standup because they're stuck versus because they're
fine.

The useful frame, six months in: agent orchestration didn't shrink the EM
job. It stripped out the part of the job that was never really management
in the first place, and left more room for the part that was.

If you're an EM experimenting with this, the highest-leverage starting
point isn't a flashy automation — it's the boring, recurring thing that
eats your attention without needing your judgment. For me that was CI and
PR triage. Find yours.
