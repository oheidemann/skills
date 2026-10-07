# Parking Lot Knowledge Base

The `parking-lot/` directory at the repo root stores ideas kept for later. An
idea here can be fully clear, even fully designed — what keeps it here rather
than in flight is that it isn't validated yet, or that acting on it now would
interfere with the current work stream. It serves one purpose: keep ideas from
being lost or re-litigated from scratch, without pretending they're already
committed.

Distinct from *deliberately out of scope* — a decision that something is ruled
out entirely, a boundary rather than a waiting room — and distinct from an open
question actively blocking real work, which belongs to a planning or grilling
session instead. See `parking-lot/README.md`, which may carry conventions local
to the repo.

## Directory structure

```
parking-lot/
├── README.md
├── channel-preferences.md
└── partner-programme.md
```

One file per **concept**, not per mention. The same idea raised three times, in
three different words, is one file, not three.

## File format

Relaxed and readable, like a short design note, not a database entry. A title,
then prose: what the idea is, what's already been figured out, what's still
open. Code or config pointers where they sharpen the idea. Short is fine — a
paragraph beats waiting until it's fully formed.

```markdown
# Concept Name

One or two sentences: what this is.

Longer if there's real substance to capture — what's already known, a relevant
pointer into the code or spec, what's still undecided. Not decided: the open
questions, named plainly.
```

### Naming the file

A short, descriptive kebab-case name for the concept: `channel-preferences.md`,
`partner-programme.md`. Recognisable enough that someone scanning the directory
knows what it is without opening it. Named for the concept, not for who raised
it.

## A parking-lot item never influences design

If filing or updating an item reveals it's already shaping a real decision —
not "we'll probably need X," but "X is nullable today because of this" — it
doesn't belong in `parking-lot/` anymore. Pull the reasoning out and make it a
proper, citable decision where it actually shapes something (an ADR, a comment
at the site), rather than recording the influence here and leaving it parked.
Parked and load-bearing are never the same file at the same time.

## When an idea graduates

Firming an idea up into a real decision happens elsewhere — a grilling session
(`/grill-with-docs`), or `/wayfinder` if it's too large for one session — never
inside `/park` itself. Once that produces a spec, an ADR, or a ticket, the
parking-lot file has done its job: delete it rather than leaving a stale
duplicate of something now recorded properly. `/park` doesn't do this step
automatically; it's a judgement call for whoever ran the session that settled
it.
