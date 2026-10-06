---
name: settle-code-review
description: "Walk a code review's remaining findings with the user one at a time, and build each decision on a review branch."
disable-model-invocation: true
---

You have been given the **open findings** of a code review: those still unsettled after the review's fixes, in this conversation's review report or a pointer to one. A finding is a reviewer's claim, not a fact.

The goal is every open finding **settled**: decided by the user, and — where the decision needs work — built and merged.

Findings are settled **one at a time**, most severe first. The user decides; you recommend. Present the next finding only once the user has decided the current one.

The user may **end the walk** at any point, leaving the remaining findings open, typically once their severity has dropped to diminishing returns. Ending the walk doesn't end the work: the decisions already made are still built, merged and cleaned up (steps 5 and 6).

Decisions that need work go to one **standing implementer**: a single **implementer subagent** on one **review branch** for the whole walk, in its own worktree, handed each decision as soon as it is made and committing each on its own. One agent on one branch keeps decisions from conflicting, and the work runs while the walk goes on.

## Steps

1. Pin the **base branch** the review was made against. List the open findings and sort them by **severity**, most severe first: how much harm each does if left as it is. Give each a **key** in that order, `F1`, `F2`, …: the user, the implementer and the final report refer to findings by key. Tell the user how many there are.

2. **Verify** the current finding against the code before presenting it: read the cited lines, their callers, and the repo's precedent for the same thing. A finding that turns out wrong or already fixed is presented as such. Then present it:

   ```
   **F<n> of <total>: <title>**

   **Finding:** <what the reviewer saw, file:line>
   **Closer look:** <what verifying showed: callers, precedent, why it is there>
   **Options:** (a) … (b) … (c) …
   **Recommendation:** <option>, <why in one or two sentences>

   <the question, naming the options>
   ```

   Wait for the user's decision. A counter-question or new idea is discussed in place; the finding stays current until decided. If the user ends the walk, go to step 5.

3. Hand a decision that needs work to the **standing implementer**:
   - The first such decision starts it: an implementer subagent in the background, on the review branch, based on the base branch. It calls the Skill tool with `tdd` for behaviour changes, commits each decision on its own, and works its queue in order.
   - Every later decision, and any amendment to one already handed over, goes to it with SendMessage: the finding's key and `file:line`, the option chosen, and what to build.
   - Tell the user in one line that it's queued, and present the next finding right away.

4. When the implementer reports, relay to the user what it did that wasn't asked for. A question it raises becomes the next item you put to the user.

5. Once every finding is settled or the user has ended the walk, wait for the implementer to finish its queue. Then the implementer merges the base branch tip into the review branch and runs the full suite. Merge the review branch into the base branch. Where a decision keeps behaviour the spec didn't ask for, add the line to the spec. Append every decision to the affected tickets' Comments, including those that leave something as it is, so the next review doesn't raise them again.

6. Remove the implementer's worktree and the review branch. Report, by key, what changed, what stays as it is, which findings were left open if the user ended the walk, and what the user still has to do.
