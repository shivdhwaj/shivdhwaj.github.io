# Always re-read the rollback plan, even when an agent wrote it

**Angle:** Lesson learned

Approved an agent-authored migration without re-reading its own rollback plan. Cost us a redeploy at 11pm. The agent wrote a good plan; I just didn't check it like I would a human's. Lesson stuck.
