---
description: Check a finished phase with your own eyes - run the tests, read the change against the spec, log what you saw
---

# /inspect

The contractor says a phase is finished: the owner tells you, or a `[done]` message arrives from
the contractor's session. You check it yourself, without waiting for approval: an inspection only
reads and runs tests. The person who did the work does
not get to be the one who checks it.

1. **What was claimed.** Read the contractor's latest session summary and state file. List what it
   says was delivered.
2. **Run the tests yourself** in the project folder, with the command recorded in
   `projects/index.md` (or in the state file). Report the real numbers: passed, failed, skipped.
   If there are no tests, that is a finding, not a pass.
3. **Read the change.** `git log` and `git diff` since the last inspection (or the files the
   summary names). Go through it against the spec (Fast track: the brief's "must have" and "out of
   scope" lists), line by line where it matters:
   - Does it do what the spec says?
   - Did anything get built that is not in the spec?
   - Are the standing decisions in `me/decisions.md` respected?
   - Anything that looks unsafe: passwords or keys in files, personal data, deleted files.
   - Secrets: if the project has a `.env` (or any file of keys), confirm `.gitignore` excludes it
     and `git log --all -- .env` is empty. Never open or print the file itself. A key that was
     ever committed must be treated as leaked: tell the owner it needs replacing.
4. **Try it** if it is something the owner can see (a page, a report, a file): open or run it and
   describe what you saw. Nothing visible yet (for example a calculations-only phase): write
   "not checked: nothing to see yet". Instead, recompute the key numbers yourself with a separate
   command and compare them with the contractor's.
5. **Write the log entry** in `supervision-log/<today>-<project>.md` using
   `templates/log-entry.md`. Separate what you checked from what you could not check.
6. **Tell the owner** in three to five plain lines: what was delivered, what you verified, what is
   wrong or open, and what you recommend next.
7. Write the next message for the contractor, `[task] Message from the supervisor:` (or `[check]`
   for a plain "accepted"): either "accepted" with what you verified and the next step, or
   exactly what must be fixed to match the approved spec or plan. If the project has no git
   history, add: start using git and commit at the end of every phase. Send it through
   `contractor-link`, which follows the owner's mode. A fix that changes the spec or the plan is a
   decision: the owner says yes first.
8. Update the project's row in `projects/index.md`.

Read-only in the project folder: run tests and read. Never fix the problem yourself.
