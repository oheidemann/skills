---
name: park
description: "File a loose idea into the repo's parking lot of things to explore later, not decided or scheduled. Finds a matching concept first; appends to it if found, creates a new file if not."
disable-model-invocation: true
---

# Park

`parking-lot/` at the repo root is the knowledge base of ideas worth remembering
but not worth deciding yet.

## Reference docs

- [PARKING-LOT.md](PARKING-LOT.md): how the `parking-lot/` knowledge base works — what belongs, file format, naming, what happens when an idea graduates

## Invocation

The user invokes `/park` and describes what they want in natural language:

- "Park this: <idea>" — file a new idea, or fold it into an existing one if it matches
- "What's in the parking lot?" — survey what's there
- "Has anyone suggested <X> before?" — check for a match without filing anything

## Survey the parking lot

Read `parking-lot/README.md` and every file beside it. Present a one-line gist
per file, grouped loosely by theme if there are more than a handful. Read-only
— nothing is written. No `parking-lot/` yet: say the lot is empty.

## File an idea

1. **Read `parking-lot/`.** Every file, not just filenames — matching is by
   concept, not keyword ("let people choose how we contact them" matches
   `channel-preferences.md` without sharing a word with it). No
   `parking-lot/` yet: create it, seeded with
   [README.template.md](README.template.md) as `parking-lot/README.md`.
2. **Check it isn't already load-bearing.** Does this idea already shape a
   real decision somewhere — a nullable field, a config left empty, a model
   kept more flexible than the current feature needs? If so, it doesn't
   belong in `parking-lot/`: say so, and point the user at pulling that
   reasoning out into a proper decision (an ADR, a comment at the site it
   shapes) instead of filing it here.
3. **Check for a match.** Does an existing file already cover this concept?
4. **No match: create one.** Follow [PARKING-LOT.md](PARKING-LOT.md)'s format —
   short kebab-case name for the concept, relaxed prose, short is fine.
5. **Match found: append, don't restate.** Fold the new angle into the existing
   file's prose if it sharpens the same idea; add it as a short addendum if it's
   a genuinely new consideration the original text didn't cover. Never create a
   second file for the same concept.
6. **Report back.** Tell the user which file was written or created, and show
   what changed.

## Not a decision

Filing something here is not a commitment and not a rejection — it's memory.
Don't grill, don't estimate, don't ask "should we build this." If the idea is
already sharp enough to want a real decision, that's a grilling session
(`/grill-with-docs`, or `/wayfinder` if it's too big for one session), not
`/park`.
