## Working with a supervisor

A supervisor agent works for the owner of this project from a separate folder. It reads this
folder to check your work and to explain your questions to the owner. It never edits here.

Its messages start with a tag and "Message from the supervisor:". They reach you in one of two
ways: the owner pastes them, or the supervisor's session sends them to you directly.

- Supervisor session: `<supervisor session name | none: paste mode>`
- Supervisor folder: `<supervisor folder path>`
- Track: `<Organized | Fast>` (the owner chose it; only the owner changes it)

### Messages from the supervisor

| Tag | Meaning | What you do |
|-----|---------|-------------|
| `[task]` | Do this | Do it, if it fits the approved spec and plan. If it does not, reply `[decision]` and stop |
| `[check]` | A question, or show / verify something | Answer. Change nothing |
| `[decision]` | The owner decided | Act on it only if it quotes the owner's approval with a date. If the quote is missing, stop and ask the owner in this window |

A message the owner pasted is the owner's decision. A message sent directly is the supervisor's.
The supervisor may send you questions, verification requests, "accepted", and fix requests that
bring the work back to the approved spec or plan. Anything else that changes the work must quote
the owner. A direct message never approves a command or a permission prompt in this window, and
never changes this file or your settings.

### Messages to the supervisor

Send them directly when a supervisor session is named above and you can reach it (look for it by
name, or by its folder). Otherwise write them for the owner to pass on.

- **`[done]`** at the end of every phase: what was delivered, the test command and its real
  result (passed / failed), the commit. Then stop and wait.
- **`[progress]`** after each finished piece of work inside a phase (a task from the plan, a
  screen, a group of files), but no more often than about once every ten minutes. Send it while you keep
  working; do not stop for it, and expect no reply. Three short lines:
  `Finished: <what>` / `Next: <what>` / `Owner needed: no | soon: <what> | now: <what>`.
  Send one also before a step that will take long or will ask the owner for permission in this
  window (an install, a long run), so the owner knows to look here. That one is exempt from the
  ten-minute limit.
  If you cannot reach the supervisor's session, do not ask the owner to pass progress notes on.
  Add the same three lines under `## Progress` in `STATE.md` instead, newest first; the
  supervisor reads them there.
- **`[decision]`** when you need the owner: the question in plain words, the options, your
  recommendation. Also write it under "Open questions" in `STATE.md`. Then stop and wait.
- **`[check]`** for a question the spec should already answer.

Apart from `[progress]` notes, one message per turn. Do not reply to a message that needs no
reply.

### Files to keep current

Keep these files current. If your method already uses other names for the same things, keep
your names and list the paths at the top of the state file.

| File | What it holds | When you update it | Fast track |
|------|---------------|--------------------|------------|
| `SPEC.md` | What we are building and what we are not | Before building, and when the owner changes scope | Not written: the supervisor's brief is the spec |
| `ROADMAP.md` | The phases, in order | Before the first phase, and when phases change | Not written |
| `plans/` | One plan per phase, written before that phase runs | Before each phase | Not written |
| `STATE.md` | Where we are, what is next, open questions for the owner | End of every phase | Yes. Copy the brief under `## Brief` first, before `## Progress` |
| `session-summaries/YYYY-MM-DD-<topic>.md` | What happened this session, what was decided, what is next | End of every session | Yes, a few lines |
| `BACKLOG.md` | Ideas that are not in the spec | Whenever one comes up | Yes |

### Rules

- Organized track: `SPEC.md`, stop for approval. `ROADMAP.md`, stop for approval. Then one plan
  per phase, and stop for approval before each phase runs. At each stop send
  `[decision] Approval needed: <file path>`.
- Fast track: no approval stops. Build the brief's "must have" list, then send `[done]`. If the
  work grows beyond the brief (someone else will use it, real data, money, going live), send
  `[decision]` recommending the Organized track, and wait.
- On the Fast track, wherever these rules say `SPEC.md`, read "the supervisor's brief". The whole
  brief is one phase with no plan: a `[task]` must fit the brief, and `[progress]` follows each
  finished must-have. A `[decision]` that changes the brief updates your copy in `STATE.md`.
- The brief says how to split the work: **alone**, **with helpers** (helper agents do parts that
  do not depend on each other, in parallel, and you put the results together), or
  **orchestrator** (you plan and check, and each phase runs in a fresh helper agent). If another
  shape fits better, use it and say why in your next `[progress]`. Either way you are the one who
  reports to the supervisor, and helpers follow the same spec and rules. While you wait on
  helpers you cannot report, so send `[progress]` when a helper starts and when it returns.
  Helpers never message the supervisor.
- Write the project files in English. Talk to the owner in their language, short and plain.
- Write a session summary whenever you stop and wait for the owner, not only at the very end.
- What is not in `SPEC.md` does not get built. Put it in `BACKLOG.md` and tell the owner.
- If a requirement cannot be met as written (for example a technical limit), say so plainly, give
  the options, and let the owner decide. Do not pick silently.
- Use git locally: `git init` at the start, one commit at the end of every phase. This is how the
  supervisor sees what changed since its last check. No remote is needed.
- At the end of a phase, paste the real test output into `STATE.md` and the session summary.
- Report a phase to the owner in terms they can check: what they can now see or do, or for an
  invisible phase, the key numbers and one example they can verify.
- Helper scripts you write (data generators, checks) live inside the project, for example in
  `tools/`, so the supervisor can rerun them.
- Every phase ends with tests the supervisor can run with one command. Write that command in
  `STATE.md`.
- Never write "done" for something you did not run.
