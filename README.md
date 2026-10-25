# Supervisor Kit

Manage software projects built by AI agents without reading code.

One agent builds. A different agent supervises: it knows you, translates every question the
builder asks into your language, helps you decide, and checks the work before you hear "done".

[עברית](README.he.md)

---

## The idea

Anyone who has built a house knows the setup. There is a contractor, with a site manager and
crews. And there is a building supervisor who works for you: knows what you asked for, reads the
plans, goes over the site log, and explains the contractor's questions in your words.

This kit does the same with agents:

- **The supervisor** lives in this folder. It knows who you are, how you work, and every project
  you run. It stays with you between projects.
- **The contractor** is a separate agent session in each project's own folder. On an organized
  project it writes a spec, a roadmap, a plan per phase, and a summary at the end of every
  session. On a fast project it builds straight from the brief.
- **You** are the CEO. You talk to the supervisor. Every decision is yours. In Claude Code the
  supervisor and the contractor message each other directly, so you stop copying and pasting;
  anything that is a decision still waits for your yes.

| | One agent for everything | Supervisor + contractor |
|---|---|---|
| Who knows you | Only the project it sits in | The supervisor, across all projects |
| Who decides what gets built | The agent building it | You, with the supervisor |
| A technical question mid-build | You answer on a hunch | The supervisor explains, then you decide |
| Who checks the work | Whoever did it | Someone who did not |

---

## What is inside

Plain text files. No software to install, no Python, no accounts.

```
supervisor-kit/
├── CLAUDE.md              the supervisor's role, rules and way of talking to you
├── SETUP.md               first-run instructions the agent follows
├── me/
│   ├── profile.md         who you are and how to explain things to you (filled at setup)
│   └── decisions.md       decisions that apply to every project
├── projects/index.md      every project, its folder, its state
├── supervision-log/       a dated log per project: delivered, checked, open
├── templates/             project brief, contractor instructions, log entry
├── .claude/commands/      the six commands below
└── .claude/skills/
    └── contractor-link/   how the supervisor talks to the contractor directly
```

**Six commands**

| Command | What it does |
|---------|--------------|
| `/add-project` | Start a new project (writes the contractor's first brief) or bring an existing one under supervision |
| `/translate` | Paste a question from the contractor. Get it in plain words, with options and a recommendation, then a ready reply |
| `/check-plan` | Before you approve a spec, roadmap or plan: is it inside the brief, and does it include the decisions you made after it was written? |
| `/inspect` | After a phase: the supervisor runs the tests itself, reads the change against the spec, and logs what it saw |
| `/watch` | While the contractor works: what changed, and whether you are needed. Once, or every few minutes |
| `/site-report` | Where every project stands, and what is waiting on you |

You do not have to remember them. Paste a contractor question and the supervisor translates it.
Say "it finished" and it inspects. Ask "what's the status?" and it looks.

**You always know where things stand (new in 1.1)**

- The contractor sends a short progress note after each piece of work. The supervisor turns it
  into one line for you: what got built, and whether it needs you: not for now, soon, or now.
- While the contractor works, the supervisor can look at the project every few minutes (you
  choose how often at setup) and tell you what changed, including when the contractor is stuck
  waiting for your approval in its own window.
- In every brief the supervisor recommends how the contractor splits the work: alone, with helper
  agents in parallel, or as an orchestrator that runs each phase in a fresh helper.

**Two tracks: organized or fast (new in 1.1)**

Not every project needs the full paperwork. A small game should not wait for a spec and a
roadmap; a system that holds customers' data should. For every new project the supervisor asks
which way you want to work, and recommends one:

| | **Organized** | **Fast** |
|---|---|---|
| Fits | Someone else will use it, real people's data, money, sending or publishing, going live, several sessions of work | A simple game or app, a one-off tool, a prototype, a single fix, something only you use |
| What the contractor writes | Spec, roadmap, a plan per phase, summaries | A state file and short summaries. The brief is the spec |
| Stops for your approval | After the spec, after the roadmap, before each phase | None. It builds and reports "done" |
| What the supervisor checks | Every plan before you approve it, every phase after | The result, against the brief |

A fast project that grows? The supervisor recommends switching to organized. Your call.

**The direct link (new in 1.1)**

The `contractor-link` skill finds the contractor's window on your computer and talks to it
directly: it sends the brief and the checks, the contractor sends back "done" at the end of each
phase, and the supervisor inspects on its own. You choose how much it may send without asking:

| Mode | What happens |
|------|--------------|
| **Standard** (recommended) | Questions, checks and fix requests go without asking, and you are told what was sent. Anything that is a decision waits for your yes |
| **Strict** | You see every message before it goes |
| **Paste** | No direct link: the supervisor writes, you copy to the contractor, as in 1.0 |

A decision is always yours, in every mode: approving a spec, roadmap or plan, answering the
contractor's questions to you, changing what gets built, deleting, spending money. You pick the
mode at setup and can change it any time by telling the supervisor.

---

## Requirements

- An agent that works on folders on your computer: **Claude Code** (in the Claude desktop app,
  the Code tab, or in a terminal), or Antigravity, Cursor, Codex and similar. The regular chat
  window cannot open a folder.
- For the direct link: Claude Code on both sides, on the same computer, version 2.1.234 or newer
  on Windows (2.1.224 on Mac and Linux). Run both windows in a mode that asks before acting (the
  usual default). Anything else works in Paste mode.

**What works where.** The kit is plain text, so the method works in any agent tool. Claude Code
adds the automation around it:

| | Claude Code | Other agent tools |
|---|---|---|
| Supervisor, briefs, two tracks, inspections, log | Yes | Yes |
| Messages between supervisor and contractor | Direct | You copy and paste |
| Progress notes | Sent to the supervisor | Written in the contractor's state file, the supervisor reads them |
| Status every few minutes | Yes (`/loop`) | When you ask |

---

## Install

1. **Extract the ZIP** somewhere easy to find, for example a `projects` folder on your drive.
   Rename the folder if you like (`my-supervisor`). The name does not matter.
2. **Open the folder** with your agent.
3. **Say:** `read README.md and SETUP.md, then start the setup`.
   It asks a few questions about you (about ten minutes) and connects your first project.
4. **Restart the session** once, so the commands load.

From then on: open this folder whenever you work on any project, and talk to the supervisor.

---

## A working day

Two windows, side by side:

| Left: the supervisor | Right: the contractor |
|---|---|
| This folder | The project's folder |
| You talk here: what you need, what you decided, "is this OK?" | The building happens here |
| Sends messages to the contractor (or writes them for you to paste) | Receives them here |
| Checks every finished phase | Writes spec, roadmap, plans and summaries (organized) or builds straight from the brief (fast), and reports "done" |

Name both windows once: `/rename supervisor` on the left, `/rename <project>-contractor` on the
right. That is how they find each other tomorrow.

With the direct link you watch both windows and step in when the supervisor brings you a
decision. In Paste mode: when the contractor asks something you are not sure about, copy it to the
left window; when it says it finished, tell the supervisor "it finished".

---

## Upgrading from 1.0

Your `me/`, `projects/` and `supervision-log/` folders hold your own information. Keep them.

1. Extract the new ZIP to a new folder.
2. Copy into your existing supervisor folder, replacing: `CLAUDE.md`, `SETUP.md`, `AGENTS.md`,
   `README.md`, `README.he.md`, the `templates/` folder and the `.claude/` folder.
   Do not copy `me/`, `projects/` or `supervision-log/`.
3. Restart the session. The first time the supervisor needs to message a contractor, it explains
   the three modes and asks which one you want. The first time it connects to a contractor, it
   asks how often you want a status, and which track each existing project is on.
4. For each project already under supervision, the supervisor offers to update the supervisor
   section in that project's `CLAUDE.md`. Say yes.

---

## The four rules

1. Every project has a track, and you choose it. Organized: a spec, a roadmap, and a summary at
   the end of each session. Fast: the brief is the spec. These are what the supervisor reads.
2. The supervisor keeps its own dated log: what was delivered, what was checked, what is open.
3. The supervisor reads the project folder. It never builds in it.
4. What is not in the spec does not get built. It goes to the backlog.

---

## How to actually use it

**Keep project folders next to this one.** `projects/my-supervisor`, `projects/crm`,
`projects/site`. Short paths, easy to find.

**Keep this folder private.** After setup it holds details about you and your projects. Do not
upload it anywhere public.

**Tell the supervisor first.** A new decision ("all prices include VAT") goes to the supervisor,
not straight to the contractor. The supervisor finds every plan it changes.

**Inspect every phase.** A phase that was not inspected is a phase you only heard about.

**The tool will change. The split will not.** Whoever builds does not check their own work, and
whoever knows you does not disappear between projects.

---

## License

MIT. Built by Rani Ifrah - [ranifrah.com](https://ranifrah.com).
