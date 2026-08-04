---
title: "The Agent on My Team: What AI-Augmented Engineering Management Actually Looks Like"
date: 2026-08-04
tags: [engineering-management, ai, developer-productivity]
---

For most of the last decade, "using AI as an engineering manager" meant asking a chatbot to help word a performance review or summarize a design doc. Useful, but marginal — it didn't touch the actual mechanics of running a team. That changed for me this year, and not in the way I expected. The shift wasn't a smarter chatbot. It was agent tooling that can act inside my team's real systems — GitHub, Jira, our CI logs, our Slack — and I started treating it less like a tool and more like a standing member of the team with a very specific, very narrow job description.

## The problem that made this concrete

Every EM has a version of this story: a PR backlog that quietly grows because reviewers are heads-down on their own work. On my team it showed up as median review time creeping past two days, engineers context-switching to review stale diffs, and me sending "hey can you take a look at this" pings that everyone (rightly) resented.

The instinct is to fix this with process — review SLAs, rotation schedules, more 1:1 nudging. I've done all of that. It helps a little and costs a lot of management attention for the return.

What actually moved the number was wiring Claude Code into our GitHub repo via MCP and giving it one job: triage every open PR before a human looks at it. Not "review the code" in the sense of judging architecture — that's still a human call. Its job was narrower: flag PRs missing test coverage, summarize the blast radius of the change, and draft first-pass comments on the mechanical stuff — inconsistent naming, missing null checks, obviously unhandled edge cases, style deviations from our conventions.

The effect was that a reviewer opening a PR now saw a pre-triaged summary and a handful of already-flagged nits, instead of a cold diff. They spent their attention on the 20% of the review that needed actual judgment: does this approach make sense, does it fit the system, is there a simpler way. Median review time dropped from about two days to same-day. My two senior engineers estimated they got back four to five hours a week that used to go into line-by-line diff reading.

## Where this actually changes the job

The time saved is the easy part to measure. The part that changed how I spend my own time as a manager is subtler.

Before, I was the aggregation layer. Before a 1:1, I'd pull open PRs, check the sprint board, skim recent Slack threads for anything on fire, and mentally assemble "what's actually going on with this person's work." Before a planning session, I'd do the same thing across the whole team. That's hours a week of context-gathering that produces zero original thought — it's pure retrieval, and it was eating the time I should have spent on the actual judgment calls: who's stuck and needs help versus who's stuck and needs to be left alone, what's really blocking the sprint versus what looks blocking on the board.

I've moved that retrieval into an agent workflow that runs ahead of these meetings — pulling PR status, ticket movement, and CI failures into a single brief. I still read it, still form my own judgment, still have the actual conversation. But I show up already oriented instead of building orientation live in the room. That's the real velocity gain: not that code ships faster (though it does), but that I stopped spending my scarcest resource — attention during a live conversation with a report — on data assembly that a tool can do correctly and faster.

## What this doesn't replace

I want to be specific about the boundary, because it's the part people get wrong in both directions. The agent doesn't decide whether a PR is good. It doesn't decide who's underperforming. It doesn't have a model of the person across the table from me in a 1:1, and it shouldn't. What it's good at is the retrieval and mechanical-flagging layer that used to consume management bandwidth without requiring management judgment. Every one of these workflows still ends with a human making the call — I've just stopped letting humans burn hours getting to the point where they can make it.

The failure mode I've seen other teams hit is treating this as "the AI will tell me what my team needs." It won't, and trying to get it to is how you end up with an EM who's outsourced the parts of the job that were the actual job. The agent triage flags what's mechanically wrong with a PR; it doesn't know that a particular engineer has been quietly struggling since a project got rescoped, or that a "small" ticket is actually the one blocking three other people out of a dependency they haven't voiced yet. That's still entirely on me.

## The practical takeaway

If you're an engineering manager and your relationship with AI tooling is still "I sometimes ask it to draft an email," you're underusing it by a wide margin. The actual leverage is in wiring it into the systems your team already lives in — your repo, your issue tracker, your CI — and giving it narrowly scoped, repeatable jobs: triage, summarize, flag, brief. Not "manage my team for me." Just: do the retrieval and mechanical work so the humans in the room, including me, spend their time on the calls that actually require a human.

We're still early in figuring out where the boundary should sit permanently. But the direction is clear enough that I'd tell any EM sitting on the sidelines: the teams that figure out this division of labor first are going to move noticeably faster than the ones that don't, and it has nothing to do with the code the AI writes and everything to do with what it frees the manager to actually manage.
