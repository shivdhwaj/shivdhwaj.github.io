---
title: "The First Ten Minutes of an Incident Aren't About Fixing Anything Anymore"
date: 2026-08-07
tags: [engineering-management, ai-tools, claude-code, incident-response, team-velocity]
draft: true
---

Last week, an on-call engineer on my team diagnosed a production incident in six minutes. Three months ago, the same class of incident would have taken closer to twenty-five — and almost none of that time would have gone into actually fixing anything. It would have gone into figuring out what was even wrong.

That gap is the story. We didn't get faster at resolving incidents. We got faster at knowing what we're looking at, and it turns out that was most of the problem the whole time.

## The problem that made this concrete

Every on-call rotation has the same shape of dread. A page fires at 2 a.m. or in the middle of a planning meeting, and the first ten minutes are pure archaeology: what deployed recently, which service actually owns this alert, has this exact failure signature shown up before, and if so what fixed it last time. None of that is diagnosis in any real sense. It's retrieval, done under pressure, usually by whoever's unlucky enough to be holding the pager.

We had runbooks. Runbooks help right up until the service they describe gets refactored and nobody updates the doc, which is to say they help for about a month after they're written and then quietly rot. By the time an incident actually needs one, it's a coin flip whether it still matches reality.

## What changed

We gave Claude Code MCP access to our deploy history, CI logs, and the incident channel's history, and one job: the moment an incident channel spins up, assemble a sourced timeline before a human has finished reading the alert. What shipped in the last two hours and to which service. What's different about this deploy versus the last five that didn't page anyone. Links to the most similar past incidents and how they were actually resolved. Anything that contradicts what the runbook currently claims, flagged explicitly rather than silently trusted.

The incident that convinced me this was worth doing wasn't dramatic — a queue backlog alert, the kind that used to mean twenty minutes of someone tailing logs and guessing. This time, by the time the on-call engineer opened the channel, there was already a note: a config change to the consumer's batch size had shipped forty minutes earlier, and the same symptom had shown up twice before, both times traced to batch-size changes interacting badly with a downstream rate limit. The fix was still a human call. But the question "what changed" was already answered.

## Where the time actually went

Mean time to diagnosis dropped from roughly twenty-five minutes to six on the incidents we've tracked since rolling this out. Full mean-time-to-resolution improved by less than that in percentage terms, which makes sense — the fix itself still takes however long it takes — but diagnosis was always the front-loaded, compressible part, and compressing it changed the character of being on call. Engineers stopped opening incident channels bracing to reconstruct context under pressure. They opened them already oriented, and spent their adrenaline on the decision instead of the digging.

## What this doesn't replace

I want to be specific about the boundary, because this is the part that's easy to get wrong in the optimistic direction. The agent doesn't decide root cause. It doesn't decide whether to roll back, flip a feature flag, or page someone else in. Those are still entirely human calls, and I'm not interested in changing that.

We had a near miss early on that made the boundary concrete. During one incident, the agent suggested a rollback target based on deploy history — reasonable, sourced, confidently stated. What it couldn't see was a manual hotfix applied through a chatops command an hour earlier, outside the normal deploy pipeline and therefore invisible to anything reading git history. The suggested rollback would have quietly undone that fix. A human caught it before acting on it, because the human was still the one deciding, not just rubber-stamping. But it was a sharp reminder that "sourced and confidently stated" is not the same thing as "complete," and the moment you stop checking is the moment that gap turns into an actual outage instead of a near miss.

## The takeaway

The pattern here is the same one I keep running into everywhere I've wired agent tooling into how the team operates: the leverage was never in the agent making the decision. It's in how much faster it gets a human to the point of being able to make one well. Runbooks that used to rot into documents nobody trusted are now the seed for a live, continuously sourced brief instead of a static page — but the account of "is this actually true" and "what do we do about it" stays with people who can be wrong and are accountable for it when they are.

If your team's incident response still starts with ten minutes of someone reconstructing context from scratch, that's not a training problem or a documentation problem you'll ever fully write your way out of. It's a retrieval problem, and retrieval is exactly what this tooling is good at. Give it the runbook and the deploy history, not just the page. Keep the judgment where it belongs.
