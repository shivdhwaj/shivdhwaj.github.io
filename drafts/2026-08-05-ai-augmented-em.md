---
title: "Three Days, Not Two Weeks: Rebuilding Onboarding Around an Agent That Already Knows the Codebase"
date: 2026-08-05
tags: [engineering-management, ai-tools, claude-code, onboarding, team-velocity]
draft: true
---

A new hire on my team shipped their first real pull request on day three this month. Six months ago, that number was closer to two weeks. The engineer wasn't slower back then — the job was. The first week or two of any engineering role is almost entirely retrieval: where does this service live, why is this table shaped the way it is, which of the four "getting started" docs is actually current this quarter. None of that requires judgment. It requires someone who already knows the answer to sit there and answer it, over and over, for every new hire, forever.

I'd been thinking about onboarding as a coaching problem for years — better docs, a buddy system, a structured 30-60-90 plan. All of that helps at the margins. None of it touches the actual bottleneck, which is that the answers to "where is X" and "why does this exist" live in senior engineers' heads and nowhere else, and getting them out requires interrupting the person who has the least time to be interrupted.

## What changed

We started giving new hires an agent on day one, not a wiki page. Claude Code, pointed at the repo with MCP access to our issue tracker and Slack history, given one narrow job: answer the orientation questions before a human has to.

Concretely, that looks like a new hire asking things like:

- Where does authentication actually happen, and why does this one service bypass the shared middleware?
- Why does this table have two `status` columns — is one of them dead?
- What's broken the last three times someone touched this queue consumer, and is there a pattern?

The agent reads the code, the commit history, and the linked tickets, and gives a sourced answer — here's the file, here's the commit that introduced the second column, here's the incident postmortem — instead of a guess. When it doesn't know, it says so instead of confabulating an explanation that sounds plausible and sends someone down the wrong path. That last part mattered more than I expected; the failure mode I was most worried about going in wasn't "too slow," it was "confidently wrong," and it's shown up rarely enough that I've stopped treating it as the primary risk.

## Where the time actually went

The obvious framing is "the agent replaced onboarding buddies." That's not what happened, and I want to be precise about it because the actual shift is more interesting.

Senior engineers didn't stop being involved in onboarding. Their time moved. Before, a new hire's questions were front-loaded with "where is X" — pure lookup, answerable from the repo, but only if you already knew where to look. Now that layer gets handled before it ever reaches a human. What reaches the senior engineer instead is the second-order question: not "where is the queue consumer" but "I read the queue consumer, here's what I think the tradeoff is with the retry logic, does that match your intent." That's a real teaching conversation. It's also the conversation senior engineers actually want to be having, instead of being pulled out of deep work eleven times a day to answer the same three lookup questions from three different new hires.

The measurable result: time-to-first-PR dropped from roughly ten working days to three. Review load on the two engineers who used to field most onboarding questions dropped noticeably — enough that they mentioned it unprompted in a retro before I asked. Neither of those numbers is about the agent writing better code. It's about the agent absorbing a category of interruption that was never actually about judgment.

## What this doesn't replace

I want to be specific about the boundary, because "AI-powered onboarding" invites exactly the wrong mental model if you let it. The agent doesn't decide whether a new hire is ramping well. It doesn't notice that someone's gone quiet in standup because they're stuck and embarrassed to ask, or that a "simple" first ticket turned out to reveal a gap in how they think about concurrency. It doesn't build the relationship that makes a new hire comfortable admitting they're lost, which is still the single highest-leverage thing a manager or buddy does in someone's first month.

What it replaces is narrower and more mechanical: the lookup layer that consumed senior attention without requiring senior judgment. That's the whole pattern, and it generalizes well past onboarding. Any recurring question that (a) has a factual, sourced answer living somewhere in your systems and (b) currently gets answered by interrupting your most senior people is a candidate. Onboarding just happens to be the version of this problem with the clearest before/after number, because you get a fresh instance of it every time you hire.

## The takeaway

If your onboarding plan is still "here's a wiki, here's a buddy, ask questions in the team channel," you're leaving a genuinely large amount of senior engineering time on the table — not because the wiki is bad, but because a static doc can't answer "why" and a busy senior engineer can't scale. Point an agent at your actual systems — code, tickets, incident history — and give new hires a place to ask the dumb questions that aren't actually dumb, they're just retrieval. Keep the humans for the part that was always the real job: judgment, context nobody wrote down, and noticing when someone's stuck before they say so.

Three days versus two weeks isn't a headline number I expected to hit this year. But it's the clearest evidence I have that the leverage in AI-augmented engineering management isn't in the code the agent writes — it's in the interruptions it absorbs so the right people can spend their attention on the part of the job that was never really retrieval in the first place.
