# Changelog

## 1.1 - 2026-10-19

**Direct link between the supervisor and the contractor.**

- New skill `contractor-link`: finds the contractor's session on the same computer, connects,
  sends messages and receives the contractor's reports. No more copy and paste.
- Three modes, chosen at setup and changeable any time: Standard (checks and questions go without
  asking, decisions wait for the owner), Strict (the owner sees every message first), Paste (as in
  1.0). A decision is always the owner's, in every mode, and is sent with the owner's words quoted.
- Message tags: `[task]`, `[done]`, `[check]`, `[decision]`. A `[done]` from the contractor starts
  `/inspect`; a `[decision]` starts `/translate` with the owner.
- The contractor's section (`templates/contractor-brief.md`) now explains direct messages, what it
  may act on, and when to report `[done]` or ask for a `[decision]`.
- Every message is logged in the supervision log, one line each.
- Falls back to Paste automatically when there is no direct link (other agent tools, another
  computer, older Claude Code).
- `README` sections: the direct link, requirements, upgrading from 1.0.

**Two tracks: Organized or Fast.**

- `/add-project` asks the owner how to work, with a recommendation. Organized: spec, roadmap and
  plans, each approved by the owner (as in 1.0). Fast: for small games, simple apps, one-off tools
  and prototypes. The brief is the spec, the contractor builds without approval stops and reports
  `[done]`, and the supervisor inspects the result against the brief.
- The supervisor recommends switching a Fast project to Organized when it grows (other users, real
  data, money, going live). The owner decides.
- The track is written in the brief, in the project's `CLAUDE.md` section and in `projects/index.md`.

**Constant supervision.**

- New tag `[progress]`: the contractor reports each finished piece of work, what is next, and
  whether the owner is needed (no / soon / now). The supervisor turns it into one line for the
  owner. Without a direct link it goes into `STATE.md`.
- New command `/watch`: what changed in the project since the last look, and whether the
  contractor is waiting for the owner in its own window. Once on request, or on a timer with
  `/loop 10m /watch`. Stops when the work is done and inspected, when the owner says stop, or
  after 7 days. When the `claude` command is available it also reads `claude agents --json` to
  see a contractor stuck on a permission prompt.
- Every look is one line under a new `## Watch` section of the supervision log, and
  `/site-report` reads it.
- The brief is sent as a `[decision]` with the owner's approval quoted. An Organized contractor
  asks for each approval with `[decision] Approval needed: <file>`, which starts `/check-plan`.
- `/inspect` and `/check-plan` know the Fast track: inspect against the brief; no plans to check.
- New setup question 8 and profile section "Status updates": every N minutes, only when something
  happens, or only when asked.
- Every brief carries a **Team** line: alone, with helpers (subagents in parallel) or
  orchestrator (a fresh helper per phase), with the reason.
- `README`: "what works where" between Claude Code and other agent tools.

## 1.0

First public version: supervisor role, setup interview, five commands, templates.
