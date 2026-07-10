# Managing Engineers When One of Your Engineers Is an Agent

Six months ago, "AI tooling" on my team meant autocomplete. Today, a meaningful share of our diffs start life as an agent's first draft — written by Claude Code, orchestrated across a handful of subagents, reviewed by a human before it ever reaches a PR. That shift hasn't just changed how my engineers write code. It's changed how I manage them.

This post is about the mechanics of that change: what actually got faster, what didn't, and what the job of an engineering manager looks like when one of the "engineers" on the team is an orchestration layer instead of a person.

## The migration that took an afternoon

The clearest example from the last few weeks: a legacy-service migration that, by our normal estimation process, was a 3-engineer-day job. Schema translation, backfill logic, edge-case handling for a handful of nullable fields nobody had touched in years, and a test suite to catch regressions.

Instead of assigning it to one engineer to grind through sequentially, we treated it as an orchestration problem. Claude Code took the target schema and our list of known edge cases, drafted the migration scripts and backfill logic, and proposed a first pass at tests. Two engineers split the review: one checked correctness against the schema, one checked the rollback story. They caught real mistakes — a few incorrect assumptions about nullable legacy fields — but catching them took an hour, not a day of writing from scratch.

We shipped by end of day. The work that used to take three engineer-days took roughly three engineer-hours of review plus the agent's compute time.

## The saved time isn't the interesting part

It's tempting to lead with the throughput number, but the number that actually changed how I plan is different: where the freed-up hours went.

In the old workflow, the engineer doing that migration would have spent most of the three days on mechanical work — writing boilerplate, re-deriving the schema mapping, writing repetitive test cases. The judgment calls (how do we handle partial failure? do we backfill in place or write-forward and cut over?) were squeezed into whatever time was left, usually at the end, under time pressure.

With the agent doing the first pass, those judgment calls came first. The engineers spent their day deciding, not typing. That's a better use of a senior engineer's time by any measure, and it's the reason I think "AI-augmented" is a more accurate term than "AI-accelerated" for what's actually happening. The tooling isn't just making the same work faster — it's reallocating attention toward the parts of the work that need a human.

## What changes for an EM

A few concrete changes to how I run the team:

**Capacity planning shifts from "hours to write" to "hours to review and decide."** Estimating a ticket used to mean estimating typing and debugging time. Now I'm estimating how much judgment the ticket requires — how many genuinely ambiguous decisions are in it — because that's the part that doesn't compress. A ticket that's mechanically large but decision-light can move very fast. A ticket that's mechanically small but full of ambiguous tradeoffs doesn't speed up much at all, no matter how good the tooling gets.

**Code review gets more important, not less.** Every agent-drafted PR still needs a human who understands the system to catch wrong assumptions — the nullable-field issue above is a good example of the kind of error that looks plausible and is wrong. I've had to be more deliberate about not letting review become a rubber stamp just because the diff looks clean and well-commented. Agents are good at producing code that reads as confident regardless of whether it's correct.

**The skill I'm hiring and coaching for is shifting.** I still want engineers who can write good code from scratch. But increasingly, the differentiating skill is being a good reviewer and orchestrator: knowing what context to hand an agent, what edge cases to flag up front, and when to stop trusting the output and go read the actual system. That's a distinct skill from raw coding speed, and it's not one our industry has historically trained for directly.

**Velocity conversations need better vocabulary.** "We shipped faster because of AI" is true and also not a useful sentence for planning. I've started tracking, informally, which categories of work compress a lot (schema migrations, boilerplate service scaffolding, test-writing for well-specified behavior) versus which don't (novel architecture decisions, anything touching an ambiguous product requirement, incident response). That distinction is doing more for my planning accuracy this quarter than any velocity metric.

## Where this is still rough

I don't want to oversell this. We're still reviewing every diff line by line. Agent output on unfamiliar parts of the codebase is noticeably worse than on well-trodden ones, and it fails in ways that look confident, which is worse than failing in ways that look uncertain. None of this replaces an engineer who deeply understands the system.

What it does is buy back the hours that used to go to mechanical work, and hand them to the humans for the decisions that actually need a human. As a manager, my job is increasingly to make sure that trade keeps happening — that the time saved goes toward better decisions, not just more tickets closed.

The teams that work out how to make that trade well are going to move at a different clock speed than the ones that don't. Figuring out exactly how is, for now, most of my job.
