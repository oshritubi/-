[decision] Message from the supervisor:
Owner approved (<YYYY-MM-DD HH:MM>): "<the owner's words>"

**Project:** <name>
**For:** <the owner, and who will use what we build>
**Track:** <Organized | Fast>
**Team:** <Alone | With helpers | Orchestrator> - <why, in one line>

## What the owner needs
<the need in the owner's words, then one line in precise terms>

## Data / inputs
<files or data the project uses, their format, and how a new version arrives. Delete if none.>

## Must have
- <...>

## Out of scope
- <...>

## Limits
- <for example: runs locally, no server, no database, no paid services>

## Standing decisions that apply
- <copied from the supervisor's decisions list>

## How we work
<Keep the paragraph of the chosen track and delete the other.>

Organized track: Write SPEC.md first and stop for the owner's approval before building. Write
ROADMAP.md after the spec is approved, and stop again for approval.
The supervisor will read SPEC.md, ROADMAP.md, each plan before it runs, STATE.md and the session
summaries, and will run the tests after every phase.

Fast track: Do not write SPEC.md, ROADMAP.md or plans. This brief is the spec: build the "must
have" list, nothing from "out of scope". Start now, keep STATE.md, commit with git, and give one
test command. When it works, send `[done]`. Stop with `[decision]` only for something this brief
does not answer. If the work turns out bigger than this brief, say so with `[decision]` and
recommend switching to the Organized track.
The supervisor will read STATE.md and the git history, and will run the tests when you report
`[done]`.

On both tracks: send `[progress]` after each finished piece of work, as your CLAUDE.md section
describes, so the owner always knows where things stand and whether they are needed.
