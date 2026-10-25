# Instructions for the agent: first-time setup

You are setting up this folder as the owner's supervisor. Read `CLAUDE.md` first so you know the
role. Then run these steps in order, in the owner's language.

Nothing here installs software. Everything is text files in this folder. The folder's name does
not matter.

If the owner writes in Hebrew, tell them once that `README.he.md` is the Hebrew guide.

---

## Step 1 - Explain in two sentences

Tell the owner what is about to happen: you will ask a few questions so you know them, and then
connect their first project. About ten minutes.

## Step 2 - Interview: who the owner is

Ask one question at a time. If the owner answers several at once, accept them and skip ahead.
Do not ask what you can already see: for language and tool, confirm instead of asking
("I'll keep talking in Hebrew and you work in Claude Code, right?").

1. What is your name, and what does your business or work do?
2. Do you have a technical background? (none / some / developer)
   This decides how you explain things, so make it easy to answer honestly.
3. Language: confirm the language they are writing in.
4. How do you like answers: short and to the point, or with the full reasoning?
5. Tool: confirm which agent tool they use for their projects.
6. Is there anything you always want, in every project? (for example: Hebrew interface,
   prices include VAT, mobile first, no paid services without asking)
7. How should I talk to the contractor? Explain first, in a few short lines:
   in Claude Code, the two windows can message each other directly, so the owner does not copy
   and paste. Then offer the three modes from `.claude/skills/contractor-link/SKILL.md`:
   - **Standard (recommended):** I send questions, checks and fix requests myself and tell you
     what I sent. Anything that is a decision (approving a plan, changing what gets built,
     deleting, spending money) waits for your yes, every time.
   - **Strict:** I show you every message before it goes.
   - **Paste:** I write the messages, you copy them to the contractor, as before.
   Say that they can change it any time by telling you. If the tool from question 5 is not Claude
   Code, the mode is Paste: say so and skip the choice.
8. While a contractor works, how often do you want a short status from me (what got built, and
   whether I need you)? Offer three answers:
   - **Every 10 minutes (recommended),** or another number they pick. Say it runs only while my
     window is open, and that each look uses a little of their usage.
   - **Only when something happens:** the contractor finishes a piece of work, or needs them.
     Offer this one only with a direct link (Standard or Strict); in Paste mode nothing reaches
     me on its own.
   - **Only when I ask.**
   If the tool from question 5 is not Claude Code, there is no timer: offer "only when I ask".

**Write each answer into `me/profile.md` as soon as you get it**, so nothing is lost if the
session drops. Write it in the owner's language, replacing the placeholders and keeping the
headings:
- "Technical background" holds the level from question 2 and what it means for explaining.
- "How to explain things to them" starts empty. You add to it over time: what worked, what
  confused them.
- "Talking to the contractor" holds the mode from question 7 and the date it was chosen.
- "Status updates" holds the answer to question 8 and the date it was chosen.

When all answers are in, change the first line to `STATUS: SET UP <today's date>`. Anything from
question 6 goes into `me/decisions.md` as dated entries. Fill the "Why" column only if they said
why; otherwise write "owner's rule".

Read the profile back in three lines and ask if it is right.

## Step 3 - The first project

Ask: do you already have a project an agent is building, or are we starting a new one?

Then run `.claude/commands/add-project.md` for it.

No project yet? That is fine. Stop here and tell the owner: when you start one, say
"new project" and I will set it up.

## Step 4 - Privacy

This folder now holds personal information about the owner and their projects. Tell them in one
sentence: keep it on your computer, and never upload it anywhere public.

If the folder is a git repository (`git remote -v` prints something) and a remote points to a
public repository, offer to remove the link (`git remote remove origin`). Do it only after a yes.

## Step 5 - Close

Tell the owner, in three short lines:
- what you now know about them,
- which project is connected (if any),
- how to work with you from now on: two windows side by side, this folder (you) and the project
  folder (the contractor). They talk to you. With a direct link, you and the contractor message
  each other and they see every message in both windows; in Paste mode, anything the contractor
  says that they are unsure about, they paste here.

Remind them to restart the session once so the commands (`/add-project`, `/translate`, `/watch`,
...) and the `contractor-link` skill load. After the restart they type `/rename supervisor` once,
so contractors can find this window. If a contractor is already working and they chose a timer,
they then type the `/loop` line again: the restart stopped it.
