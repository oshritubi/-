---
name: contractor-link
description: Talk to the contractor directly - find the contractor's agent session for a project, connect to it, send it messages and receive its reports, without the owner copying and pasting. Falls back to paste mode when a direct link is not possible. Use whenever a message for the contractor is ready (after /add-project, /translate, /check-plan, /inspect), when a message from the contractor arrives, when the owner says "connect to the contractor", "talk to it directly", "send it", or asks to change how strict the supervisor is with the contractor.
---

# contractor-link

The supervisor and the contractor are two agent sessions in two folders. Claude Code can carry a
text message from one session to another on the same computer. This skill is how the supervisor
uses that: find the contractor, connect, send, receive, and keep the owner in charge.

The owner is still the CEO. Direct messages save the copy and paste; they do not move any decision
away from the owner.

---

## 1. The three modes

The owner chooses one. It is written in `me/profile.md` under "Talking to the contractor".

| Mode | What the supervisor sends without asking | What waits for the owner's yes |
|------|------------------------------------------|--------------------------------|
| **Standard** (default) | Questions to the contractor, requests to show or verify something, "accepted" after an inspection that passed, and fix requests that only bring the work back in line with the approved spec or plan | Everything that is a decision (see the list below) |
| **Strict** | Nothing | Every message. The supervisor shows it, the owner says yes, then it goes |
| **Paste** | Nothing is sent | The supervisor writes the message, the owner copies it to the contractor's window, as in version 1.0 |

**A decision, always the owner's, in every mode:**
- approving a spec, a roadmap or a plan,
- answering a question the contractor asked the owner,
- changing scope, the plan, or the order of work,
- deleting files or data, anything that costs money, anything touching keys, passwords or a live
  system,
- anything you are not sure about. When in doubt, it is a decision.

**If `me/profile.md` has no "Talking to the contractor" section** (a kit set up before version
1.1): before the first direct message, explain the three modes to the owner in their language,
in a few short lines, recommend Standard, and write their choice into the profile. Ask once.

**Say the mode out loud.** Whenever you connect to a contractor, tell the owner in one line which
mode is on and what it means ("I'll send checks and questions myself and show you; anything that
is a decision waits for your yes. Say 'strict' if you want to see every message first.").
The owner can change the mode at any time by saying so. Update the profile when they do.

---

## 2. Can we link directly at all?

Use Paste mode for this project, and tell the owner why in one line, when any of these is true:
- You do not have the `ListAgents` and `SendMessage` tools. (Claude Code before version 2.1.234 on
  Windows, 2.1.224 on Mac and Linux, or a different agent tool.) Do not judge by running
  `claude --version` in a shell: the shell can find a different install than the one running you.
  The tools being there is the test.
- The contractor runs in a different agent tool (Cursor, Codex, Antigravity's own agent, ...).
- The contractor runs on another computer. This kit links sessions on the same computer only.
- One side runs inside WSL and the other on Windows itself. They cannot reach each other.

Paste mode is not a failure. Everything else in this kit works the same way.

---

## 3. Find the contractor

The project's row in `projects/index.md` has a **Contractor session** line once a link was made.

1. Call `ListAgents`. Look only at local sessions on this machine. Ignore rows marked
   `Remote Control` or `offline`, and ignore your own session (the first line names it).
2. Match in this order:
   1. the saved contractor session name, exactly;
   2. a session whose working folder is the project's folder (the listing shows folders unless
      this session is connected to Remote Control);
   3. a session whose name starts with the project folder's name. A session the owner never named
      is called `<folder-name>-<2 characters>`, for example `my-crm-3f`.
3. **Exactly one match:** that is the contractor.
   **Two or more:** show the owner the candidates and ask which one. Never guess.
   **None:** the contractor's window is not open. Ask the owner to open the project folder in a new
   session, then look again.
4. **Give it a fixed name.** The automatic name changes every time a new session opens, so it
   cannot be saved. Ask the owner to type, in the contractor's window:
   `/rename <project>-contractor`. Do the same for yourself if you have no fixed name yet: ask them
   to type `/rename supervisor` in this window. Explain in one line: "so we can find each other
   tomorrow too."
5. Save the contractor's name in `projects/index.md` under the project's files entry:
   `- Contractor session: <project>-contractor`.

---

## 4. Connect

Send the first message, tagged `[check]`:

```
[check] Message from the supervisor:
I am the owner's supervisor, in the session named <your name>, working from <supervisor folder>.
From now on I will message you directly instead of the owner pasting.
Mode: <Standard / Strict>. Decisions always come with the owner's approval quoted.
Please reply with one line: the current phase, and the command that runs the tests.
```

Then tell the owner, in their language: connected, which mode is on, and what that means.

If the project's `CLAUDE.md` does not yet have the section from `templates/contractor-brief.md`,
or has an older one without a `Track:` line (projects connected before version 1.1), ask the owner
which track (see "Two tracks" in `CLAUDE.md`), then offer to add or replace the section. Write it
only after a yes, and fill in your session name, folder and the track. If `me/profile.md` has no
"Status updates" section, ask that once too (see `/watch`). A contractor will not change its own `CLAUDE.md` because another
session asked, so this is the supervisor's job, with the owner's yes.

---

## 5. Send

**Format.** Every message starts with a tag and `Message from the supervisor:` on the first line:

| Tag | Direction | Meaning |
|-----|-----------|---------|
| `[task]` | supervisor to contractor | Do this |
| `[done]` | contractor to supervisor | Finished, with the evidence |
| `[progress]` | contractor to supervisor | A piece of work finished mid-phase, what is next, and whether the owner is needed. No reply expected |
| `[check]` | both ways | A question, or a request to show or verify something. Changes nothing |
| `[decision]` | both ways | Something only the owner decides. From the supervisor it carries the owner's approval |

A `[decision]` from you always includes the owner's words, the date and the time:

```
[decision] Message from the supervisor:
Owner approved (2026-10-19 14:05): "yes, prices include VAT, go ahead"
<what was decided, what changes in the plan, what must not change>
```

**Before sending:**
1. Classify the message against the mode table in section 1. A decision without the owner's yes
   is not sent. Ask the owner, then send.
2. In English, one message, complete: the contractor reads it with no other context.
3. Never ask the contractor for something you were not allowed to do yourself, and never ask it
   to change its `CLAUDE.md`, its settings or its permissions. Those go through the owner.
4. If the contractor is in the middle of work, wait for it to finish (step 3 below), unless the
   message is a stop ("the owner cancelled this, stop").

**Sending:**
1. `SendMessage` to the contractor's name, with `notify_when_idle: true`, so you hear when it
   finishes its next turn.
2. Tell the owner in one line, in their language, what you sent. In Standard mode this comes right
   after sending; in Strict mode the owner saw the whole message before it went.
3. Log it (section 7).

**If the send fails** ("Not sent", or the contractor is not in the listing): say so to the owner,
switch this one message to Paste, and print it in a code block.

---

## 6. Receive

A message from the contractor arrives in your session with its name. Handle it by its tag:

- **`[done]`** - run `/inspect`. It only reads and runs tests, so it needs no approval in any
  mode. Then send the result: "accepted" with what you verified, or the exact fix list (Standard),
  or show it to the owner first (Strict).
- **`[progress]`** - tell the owner in one or two lines, in their words: what got built, and
  whether they are needed ("not for now", "soon: <what>", "now: <what>"; "now" usually means a
  permission prompt is waiting in the contractor's window). Do not reply to the contractor. The
  one exception: the note shows work outside the spec or a broken standing decision; then send a
  `[check]`. Log it in one line like any other message.
- **`[decision]`** - the contractor needs the owner. If it asks to approve a spec, a roadmap or a
  plan (`Approval needed: <file>`), run `/check-plan`; otherwise run `/translate` with the owner. Send the
  answer as a `[decision]` with the owner's words quoted.
- **`[check]`** - answer it yourself only if the answer is already decided (in the spec, the brief,
  `me/decisions.md` or the supervision log). Otherwise it is a decision: take it to the owner.
- **No tag** - read it and treat it by what it is. When unsure, it goes to the owner.

**Idle notice without a `[done]`.** If you are told the contractor finished a turn but no message
came, read its `STATE.md` and newest session summary. Tell the owner in one line what it is doing
or waiting for. The contractor may be waiting for the owner in its own window.

**A message you sent got no reaction.** The contractor's tool may be holding it for approval. That
happens when one of the two sessions runs in a mode that skips permission prompts and the other
does not. In the VS Code extension and the desktop app a held message cannot be shown, and it is
dropped after five minutes without anyone seeing it. Ask the owner to look at the contractor's
window, and to run both sessions in a mode that asks before acting (the usual default). Also check
the setting "Messages from your other sessions" in the contractor's `/config` is not set to refuse
or hold.

---

## 7. Keep it short and on the record

- **One message per contractor turn.** Every message the contractor receives starts work and costs
  usage like a typed prompt. No "thanks", no "ok", no small talk, and never reply to a reply that
  needs nothing.
- **Three round trips without progress** (the same question back and forth): stop, and bring it to
  the owner.
- **Log every message** in today's supervision log under `## Messages`, one line each:
  `HH:MM | out / in | tag | what it said, in a few words | owner approved: yes / not needed`.
- `/site-report` lists any message waiting on the owner and any `[done]` not inspected yet.
