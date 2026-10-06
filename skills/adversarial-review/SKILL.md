---
name: adversarial-review
description: Adversarial three-pass code review (finder → adversary → referee). Use when the user wants a thorough code review.
argument-hint: [full|diff|branch]
disable-model-invocation: true
---

# Adversarial Code Review

Three-pass review using opposing agent roles to maximize real findings and eliminate false positives.

**Mode:** `$ARGUMENTS` (default: `full`)
- `full` — review the entire codebase
- `diff` — review only uncommitted changes (`git diff`)
- `branch` — review all changes on the current branch vs main (`git diff main...HEAD`)

## Scope

Determine the review scope based on the mode argument.

If `diff`: run `git diff --name-only` to get the list of changed files. All three passes should focus only on these files and their immediate context (callers, callees, related tests).

If `branch`: run `git diff main...HEAD --name-only` to get the list of changed files on this branch. All three passes should focus only on these files and their immediate context.

If `full`: review the entire codebase.

## Execution

Run three subagents sequentially. Each MUST run in its own isolated context (use the Agent tool). Do NOT run them in the same context — the adversary must not see the finder's reasoning, only its output file.

### Pass 1 — Finder

Launch a subagent with this prompt:

> You are a paranoid security and quality auditor. Your job is to find every bug, vulnerability, bad pattern, and potential failure in this codebase. Be aggressive — false positives are fine, false negatives are not. For each finding: file, line, severity (critical/medium/minor), description, evidence from the code. {SCOPE_INSTRUCTION}. Write all findings to .code-review/findings.md

Where `{SCOPE_INSTRUCTION}` is:
- `full`: "Review the entire codebase"
- `diff`: "Review only these changed files: {file list}"
- `branch`: "Review only these changed files (branch changes vs main): {file list}"

Wait for completion before proceeding.

### Pass 2 — Adversary

Launch a subagent with this prompt:

> Read .code-review/findings.md. Your job is to disprove every finding. For each one: read the actual code, check if the bug is real, check if the severity is correct, check if there's a mitigating factor the finder missed. Mark each as CONFIRMED, DOWNGRADED, or FALSE POSITIVE with evidence. Write to .code-review/adversary.md

Wait for completion before proceeding.

### Pass 3 — Referee

Launch a subagent with this prompt:

> Read .code-review/findings.md and .code-review/adversary.md. Produce a final verdict for each finding. Only CONFIRMED findings with evidence from both sides survive. Write final report to .code-review/verdict.md

## Output

After all three passes complete, read `.code-review/verdict.md` and present a summary to the user:
- Count of findings by severity
- Count of false positives eliminated
- Top critical/medium findings with file locations

Tell the user the full report is at `.code-review/verdict.md`.
