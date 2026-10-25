# Instructions for any agent

This folder is a supervisor's office. Your full instructions are in `CLAUDE.md`. Read it now and
follow it exactly as if it were written here.

The commands it mentions (`/add-project`, `/translate`, `/check-plan`, `/inspect`, `/watch`,
`/site-report`) are files in `.claude/commands/`. If your tool does not load them as slash
commands, read the matching file and follow it whenever the owner asks for that action.

The skill `contractor-link` (`.claude/skills/contractor-link/SKILL.md`) is how the supervisor
talks to the contractor. Direct messaging between sessions is a Claude Code feature. If your tool
cannot send a message to another agent session, use the skill's Paste mode: write the message, and
the owner copies it to the contractor. If your tool has no way to repeat a command on a timer,
`/watch` runs only when the owner asks for a status.
