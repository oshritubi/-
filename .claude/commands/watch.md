---
description: A look at a contractor while it works - what changed since the last look, and whether the owner is needed. Run once, or every few minutes with /loop
---

# /watch

A status, not an inspection. It only reads: no tests, no messages to the contractor, nothing
written in the project folder. Say "built" or "written", never "works", until `/inspect` checked it.

## Which project

The one the owner named. Otherwise every project whose contractor is working: it was sent a brief
or a task, has not answered `[done]` since, and is not waiting on a `[decision]` it sent (that one
waits for the owner, and you already told them). If no contractor is working, say so in one line
and stop the timer (see "Stopping").

## One look

1. **Where the last look ended:** the newest line under `## Watch` in the project's newest
   supervision log. No such line: start from the last inspection.
2. **What changed since then.** Use commands, not your eyes:
   - in the project folder: `git log --oneline` for commits since that time, and `git status --short`
     for work not committed yet;
   - the files changed since that time, newest first;
   - `[progress]` notes that arrived since then, and the "Progress" lines at the top of `STATE.md`.
3. **Is the contractor waiting for the owner?**
   - A `[progress]` or `[decision]` that says "now".
   - If the `claude` command works in your shell: run `claude agents --json` and find the
     contractor's session by its name or its folder (`cwd`). `"status": "waiting"` with
     `"waitingFor": "permission prompt"` or `"input needed"` means it is waiting for the owner in
     its own window. If the command fails or the session is not in the list, skip this check. Do
     not guess.
   - Nothing changed for two looks in a row and no `[done]`: it may be waiting on a prompt in its
     own window. Say it as a possibility: "take a look at its window".
4. **Tell the owner,** in their language:
   - Waiting for them: say that first, and what it is waiting for.
   - Something changed: two or three lines. What got built, in their words. What is next. Owner
     needed: no / soon: what / now: what.
   - Nothing changed: one line. "Still working on <what>, nothing needed from you."
   - Never repeat what a `[progress]` note or an earlier look already told the owner. Say only
     what is new since then.
5. **Log one line** under `## Watch` in today's supervision log (see `templates/log-entry.md`).

If you see a problem (work outside the spec, a standing decision broken), tell the owner and
handle it with `contractor-link` in the owner's mode. `/watch` itself never messages the
contractor.

## On a timer

How often is the owner's choice, under "Status updates" in `me/profile.md`. If that section is
missing (a kit set up before this command existed), ask once, recommend every 10 minutes, and
write the answer there.

- **Every N minutes:** uses Claude Code's built-in `/loop`. Ask the owner to type this in your
  window, and print it so they can copy it: `/loop 10m /watch` (with their number). Tell them
  once, in a few plain words:
  - it runs only while this window stays open, and only when you are free, so a look can come a
    few minutes late;
  - each look uses a little of their usage;
  - it stops by itself after 7 days, and they can stop it any time by saying "stop the watch".
- **Only when something happens:** no timer. The updates are `[progress]`, `[decision]` and `[done]`.
- **Only when asked:** nothing automatic. The owner asks "what's the status?" whenever they like.
- **Paste mode in Claude Code:** the timer works the same way, and it is the only live view,
  since progress notes then sit in the contractor's `STATE.md` until you look.
- **Another agent tool:** there is no `/loop`. The owner asks "what's the status?", and you run
  one look.

Whenever you send a contractor new work (a brief, an approval, a fix list) and the owner chose a
timer that is not running, remind them of the line in one sentence.

## Stopping

Stop the timer and tell the owner in one line when:
- the contractor reported `[done]`, you inspected it, and no new work was sent;
- the owner says stop;
- three looks in a row found nothing new, and `claude agents --json` shows the contractor idle
  (not waiting). If you could not run that check, do not stop: tell the owner once "nothing has
  moved for a while, take a look at its window", and keep looking.

How: a timer started as `/loop 10m /watch` is a scheduled task. Cancel it with `CronList` (find
the `/watch` task) and `CronDelete`. A `/loop /watch` without a number is self-paced: stop it with
`ScheduleWakeup` and `stop: true`. If you cannot cancel it yourself, tell the owner to press `Esc`
(self-paced) or to close and reopen this window.
