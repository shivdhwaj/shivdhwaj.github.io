# Weekly Content Routine Prompts

Scheduled-routine prompts for Shivdhwaj Pandey's personal content pipeline
(AI-augmented engineering management). Each file below is the full stored
prompt for one scheduled routine in Claude Code.

| Routine | File | Schedule | Output |
|---|---|---|---|
| Blog (Substack) | `blog-weekly.md` | Monday ~7:00 IST | 1 essay → `blog/` |
| Twitter/X | `twitter-weekly.md` | Monday ~8:00 IST (after blog) | 7 tweets → `twitter/` |
| LinkedIn | `linkedin-weekly.md` | Tuesday ~8:00 IST | 2 posts → `linkedin/` |

All three routines work in the `shivdhwaj/social_media` repository and commit
directly to its default branch. No Gmail, Slack, branches, or PRs involved.

Supporting material:

- `x-engagement-playbook.md` — the manual daily X engagement play (target
  accounts + reply method) that the routines cannot do automatically.

Setup checklist before scheduling:

1. The Claude Code environment must have `shivdhwaj/social_media` in its
   GitHub repository scope.
2. Create `notes/ideas.md` in `shivdhwaj/social_media` and jot real wins,
   numbers, and anecdotes there — the routines only use real metrics from
   that file.
3. Schedule in the order shown above so the blog draft exists before the
   Twitter and LinkedIn runs read it.
