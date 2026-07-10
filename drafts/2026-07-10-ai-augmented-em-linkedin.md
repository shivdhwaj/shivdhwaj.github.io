Two weeks ago, a migration that would've eaten 3 engineer-days took one afternoon.

Not because we found a shortcut in the migration itself. Because we changed who — or what — does the first pass.

We pointed Claude Code at the legacy service, gave it the target schema and a list of edge cases we already knew about, and let it draft the migration scripts, backfill logic, and a first cut of tests. Two engineers reviewed, corrected the assumptions the model got wrong (there were a few — mostly around nullable legacy fields), and shipped by end of day.

The interesting part wasn't the time saved. It was where the engineers' attention went. Instead of writing boilerplate, they spent the day on the two decisions that actually mattered: how to handle a partial-failure rollback, and whether we should backfill in place or write-forward. That's the work I want senior engineers doing.

As an EM, this is changing how I think about capacity planning. The bottleneck on a lot of our tickets was never "can we code this" — it was context-switching and grunt work eating the hours where real judgment happens. Agent tooling doesn't replace that judgment. It buys back the hours to use it.

The teams that figure out how to delegate the right 70% to an agent — and keep humans firmly on the 30% that requires taste — are going to move at a different clock speed than everyone else.

Still early days. Still reviewing every diff. But the shape of the job is shifting.

What's the first workflow you handed to an agent that actually stuck?
