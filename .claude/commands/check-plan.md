---
description: Read the contractor's spec, roadmap or plan before the owner approves it, and catch what is missing, outdated or out of scope
---

# /check-plan

Run this whenever the contractor stops for approval: after the spec, after the roadmap, and before
each phase runs. This is the Organized track. A Fast project has no spec or plans to check; if a
Fast contractor wrote one anyway, tell the owner the project may have outgrown the Fast track.

1. Find what is waiting for approval: the spec, the roadmap, or the newest file in the plans
   folder. Say which file you are reading.
2. Read it against:
   - **the brief** (`projects/<project>-brief.md`): is every "must have" there? Did anything from
     "out of scope" sneak in?
   - **the spec** (for a roadmap or plan): is everything in the plan inside the spec? Is anything
     from the spec missing that should be in this phase?
   - **decisions made after it was written**: `me/decisions.md` and the decisions in the
     supervision log. Compare dates. This is where most gaps hide.
   - **the previous phase's result**: does the plan build on what actually exists, or on what was
     planned?
   - **questions the contractor asked the owner**: explain each one (as in `/translate`) with
     options and a recommendation.
3. Report to the owner in plain words:
   - "Fine to approve", or
   - the gaps, each in one line with why it matters.
4. Write the reply for the contractor, starting with `[decision] Message from the supervisor:`:
   the approval, the answers to its questions, and exactly what to change, if anything. Approving
   is always the owner's decision: send it through `contractor-link` only after the owner's yes,
   with their words quoted (or the owner pastes it, in Paste mode).
5. Log it in today's supervision log: what you checked, your recommendations, and the owner's
   answer once they give it (until then: "waiting on the owner"). List any additions the
   contractor made beyond the brief, with your keep/remove recommendation; the owner decides.

Do not rewrite the document yourself and do not edit any file in the project folder.
