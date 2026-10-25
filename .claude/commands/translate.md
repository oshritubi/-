---
description: Explain a contractor's question in the owner's language, help decide, and write the answer back to the contractor
---

# /translate

The owner pasted something the contractor said, or a `[decision]` message arrived from the
contractor's session: usually a question or a request for approval.

1. **Which project?** If it is not obvious, ask. Read that project's spec and state file so you
   understand the question in context.
2. **Explain it** at the level `me/profile.md` describes:
   - What the contractor is asking, in one or two plain sentences.
   - Why it matters: what changes for the owner depending on the answer.
   - The options, two or three, each with what it costs or risks.
   - Your recommendation and the reason, in one line.
   - If it is a request to approve a command: what the command does, and whether it is safe.
3. **Check it against the rules.** Does any option break a standing decision in `me/decisions.md`
   or go outside the spec? Say so.
4. **Wait for the owner's decision.**
5. **Write the reply for the contractor**, starting with `[decision] Message from the supervisor:`,
   complete in one message, with the owner's words quoted. Include what was decided and anything
   that must not change. Send it through `contractor-link` (or the owner pastes it, in Paste mode).
6. If the decision applies beyond this project, add it to `me/decisions.md`.
7. Add a short entry to today's supervision log: the question, the decision.

If the question is one the owner does not need to decide (a purely technical choice with one
sensible answer), say so, recommend the answer, and still let the owner confirm.
