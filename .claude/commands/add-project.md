---
description: Bring a project under supervision - a new one (write the contractor's first brief) or an existing one (map its files)
---

# /add-project

Ask first: **new project, or one that already exists?**
A project whose folder exists with some files or data, but no agent has worked on it yet, counts
as new: do not create the folder, and look inside it without changing anything.

## A new project

1. Ask the owner, in plain words. Small questions can go together in one message:
   - What do you need? (let them describe it freely)
   - Who will use it?
   - What must it do on day one? What can wait?
   - Any limits? (budget, no server, must run on their computer, a deadline)
   - Will the data change over time? How does a new version arrive?
   Anything with one sensible answer: do not ask. Choose it, and list it in the summary in step 5
   so the owner can correct it.
2. **Ask which track** (see "Two tracks" in `CLAUDE.md`), in one plain question with your
   recommendation based on the answers so far. For example: "Do you want this organized, with a
   spec and a roadmap you approve before anything is built, or fast, where the contractor builds
   straight from this brief and I check the result? For a game only you will play, I recommend
   fast." Do not choose silently. If the owner has a standing preference in `me/decisions.md`,
   say it and confirm it fits this project.
3. If the owner gave you data or files, look at them (read-only). Check them against
   `me/decisions.md`. A conflict (for example amounts before VAT when the rule is "prices include
   VAT") is a decision for the owner now, before the contractor starts. Any count or total you
   report comes from a command, not from reading.
4. Read `me/decisions.md`. Every standing decision that touches this project goes into the brief.
5. Fill `templates/project-brief.md` and save it as `projects/<project-name>-brief.md` (never over
   the template). Keep only the "How we work" paragraph of the chosen track. On the Fast track the
   brief is the spec, so its "must have" and "out of scope" lists must be complete and checkable.
   Fill the **Team** line with your recommendation (see "The contractor's team" in `CLAUDE.md`).
   Show the owner a summary in their language, three to five lines including the track and the
   team, and ask for a yes. The brief itself stays in English.
6. If the folder does not exist yet, ask where it should be. Suggest a sibling of this folder:
   `../<project-name>`. Create it only after a yes.
7. Offer to add the supervisor section to the project's `CLAUDE.md`: the content of
   `templates/contractor-brief.md`, with the track filled in. Explain in one line: this tells the
   contractor which files to keep so you can read its work. If the project has no `CLAUDE.md`, the
   section becomes the whole file. Fill in your session name and this folder's path in it. Write
   it only after a yes. This is the only time you write inside a project folder.
8. Hand the brief to the contractor (`contractor-link`):
   - Ask the owner to open a new agent session in the project folder, and to type
     `/rename <project-name>-contractor` there.
   - Connect and send the brief directly. The owner already said yes to it in step 5, so this is
     approved: fill its "Owner approved" line with their words and the time. Tell the owner the
     mode (see `contractor-link`).
   - No direct link possible: tell the owner to paste the brief, and **print the full brief in
     your reply inside a code block** so they can copy it in one go.
   - Organized track: the contractor's spec comes back to you for `/check-plan` before anyone
     approves it. Fast track: the next thing you expect is `[done]`, then `/inspect`.
   - Start the watch the way the owner chose under "Status updates" in `me/profile.md` (see
     `/watch`). If that section is missing, ask now.

## An existing project

1. Ask for the folder path. Confirm it exists.
2. Look around without changing anything: list the top level, read `CLAUDE.md` / `README` if
   present, look for a spec, roadmap, plans, state file, session summaries, backlog, and how
   tests run.
3. Report in plain words what you found and what is missing. Ask which track (as in step 2 of a
   new project). Organized: a missing spec or roadmap is the first thing the project needs, and
   the contractor writes it from what exists. Fast: write a short brief from what exists
   (`projects/<project-name>-brief.md`) and get the owner's yes; it becomes the spec. On both
   tracks a missing state file or test command comes first, because without them you cannot
   supervise it.
4. Offer to add the supervisor section to the project's `CLAUDE.md`
   (`templates/contractor-brief.md`, with your session name, this folder's path and the track),
   only after a yes.
5. If a contractor session is open on the project, connect to it (`contractor-link`).
6. Send the next step as a `[decision]` with the owner's yes quoted: on Fast, the brief from step
   3; on Organized, "write SPEC.md from what exists and stop for approval" (or the missing files).
   No direct link: print it in a code block for the owner to paste.

## Both

- Add a row to `projects/index.md` (with the track) and a "Where each project keeps its files"
  entry with the real paths, the test command and, once connected, the contractor session name.
- Create `supervision-log/<today>-<project>.md` with one entry: project added, what exists, what
  is missing.
