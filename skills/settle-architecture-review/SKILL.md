---
name: settle-architecture-review
description: "Walk an architecture review's candidates with the user one at a time, then summarise the decisions for /to-tickets."
disable-model-invocation: true
---

You have been given the **candidates** of an architecture review: in this conversation's review, or a pointer to its report. A candidate is a reviewer's claim, not a fact.

The goal is every candidate **settled**: decided by the user as a **ticket**, **left**, or **folded** into an earlier ticket decision, whole or in parts. Decisions live in this conversation; the walk writes nothing to the repo. At the end, the **decisions summary** indexes them for `/to-tickets`, which reads the walk for the detail.

The review is **ephemeral**: its report sits in a temp folder and the walk in this conversation, and nothing carries either forward once the run ends. Only the tickets outlast it. A candidate left, or still open when the walk ends, is dropped with them, and that is fine: improvement is steady, and the next review finds again whatever still matters.

Candidates are settled **one at a time, in the review's order**. The user decides; you recommend. Present the next candidate only once the user has decided the current one.

The user may **end the walk** at any point, leaving the remaining candidates open. The decisions already made still go into the summary (step 4).

## Steps

1. Read the repo's **triage labels**: the `## Agent skills` block in `CLAUDE.md` or `AGENTS.md` points to them. If it doesn't, tell the user to run `/setup-matt-pocock-skills`. List the candidates in the review's order and give each a **key**, `C1`, `C2`, …: the user and the summary refer to candidates by key. Tell the user how many there are.

2. **Verify** the current candidate before presenting it: read the code it cites, its callers, the commits that shaped it, and any open ticket already on it. What an open ticket already covers, recommend to leave, naming that ticket. Then hold it against the decisions already made: an earlier ticket may take part of it, or leave part of it moot. Every claim you present cites code you read, and so does every part your recommendation names, a part split off or folded included. Then present it:

   ```
   **C<n> of <total>: <title>**

   **Candidate:** <what the review claimed>
   **Closer look:** <confirmed, narrower, wider, or not confirmed: what verifying showed, file:line>
   **Recommendation:** <per part where it splits: ticket at <triage label>, leave, or fold into C<k> or a part of it>, <why in one or two sentences>

   <the question>
   ```

   For a ticket, say what it would change, what it touches, and which documented rule it revises, if any; name what it leaves open. Recommend the agent-ready label where the closer look leaves nothing open, the needs-evaluation label otherwise. Recommend a split where the parts differ in what they wait for, in triage label, or in what they revise; size alone is no reason. Wait for the decision. A counter-question is discussed in place; the candidate stays current until decided. If the user ends the walk, go to step 4.

3. Record the decision in one line and present the next candidate:
   - **Ticket**, with its triage label: an entry of its own in the summary. How many tickets it becomes is for `/to-tickets` to decide.
   - **Left**: the key and the word, nothing more.
   - **Folded into `C<k>`**, or into a part of it, `C<k>a`: that earlier ticket takes on the folded part. Only a ticket takes a fold.

   A candidate split into parts gives each part its own outcome; each part that is a ticket gets its own key, `C<n>a`, `C<n>b`, ….

4. Once every candidate is settled, or the user has ended the walk, give the **decisions summary**:

   ```
   **Tickets**
   - **C<n> · <title>.** `<triage label>`. <the decision in one line>. *Revises* …; *Open:* …; *Folded in:* …; *After* C<k>; *Overlaps* C<k>: … (each only where it applies)

   **Left:** <keys; for a candidate split between left and folded, the folded part in brackets, e.g. C4 (its cache part folded into C2)>
   **Still open:** <keys, or none>

   Next: `/to-tickets`.
   ```
