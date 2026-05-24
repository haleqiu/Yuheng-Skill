---
name: code-review-neat-clean
description: Review and refactor code toward minimal, fail-fast, no-dead-path style. Use when users ask to clean code, reduce conditions/variables, simplify data flow, remove unused modes, review commits/branch diffs, or generate code-review question checklists.
---

# Code Review Neat Clean

## Intent

Apply a strict "less is more" style:
- keep behavior correct
- reduce branches and temporary variables
- fail fast on invalid states
- remove dead or unreferenced paths

This skill is for cleanup and review, not feature expansion.

## Core Principles

1. Fail fast, do not silently continue on invalid config/data.
2. Remove unused modes/paths when confirmed unused.
3. Avoid over-abstraction: one-line helpers should stay inline.
4. Keep data flow top-down and obvious (policy first, execution after).
5. Minimize control flags that are always constant.
6. Keep naming concrete (`start_frame`, `end_frame`, `duration`) and avoid redundant aliases.
7. Check naming for clarity: flag names that are misleading, ambiguous, or overly complex. Prefer short, obvious names over long compound ones (e.g. `skip` over `start_skip_frames_offset_value`). A name should be understandable without reading surrounding code.
8. Preserve behavior unless user explicitly asks for behavior changes.
9. Module location should reflect ownership, not convenience. Ask: if this design decision changes, which module is responsible? The code should live there.
10. A wrapper function that only dispatches (`return f(x) if mode == 'y' else None`) is a deferred `if` at the call site — inline it there instead.
11. Two functions that share logic but differ only in a mode flag should be one function; the caller owns the dispatch decision.
12. Backward-compatibility shims must have a clear owner and expiry. If no callers exist in the repo, delete them.

## Review Workflow

1. Map execution flow.
   - Identify where values are produced, transformed, consumed.
   - Mark branch points by mode/config.

2. Flag cleanup opportunities.
   - Dead branch/mode (not referenced by configs/scripts/tests).
   - Duplicate checks in multiple places.
   - Temporary variables used once.
   - Policy variables assigned far from use.
   - "Warn and continue" where invalid state should raise.
   - Names that mislead, shadow, or are unnecessarily long/complex.
   - Module imports logic it does not own (e.g. training file importing from model internals to assemble a tensor the model should produce itself).
   - Two files importing the same things and producing similar outputs — ask who owns the boundary.
   - A function whose only job is to wrap another function with a mode check — that check belongs at the call site.

3. Propose minimal edits.
   - Prefer small, local diffs.
   - Keep one behavior change per cleanup item.
   - Add focused tests only when behavior contracts change.

4. Verify.
   - Run targeted tests first.
   - Run lints for touched files.
   - Confirm no accidental behavior drift in hot paths.

## Output Style For Reviews

Return findings first, ordered by severity:
- Critical: bug/regression/invalid-state handling
- Important: maintainability/readability issues
- Optional: polish

When summarizing differences or changed behavior, always cite the exact code
location: file path plus line number or line range. Prefer concise references
such as `PGO/Graph/factor_graphs.py:432` or
`PGO/Graph/factor_graphs.py:432-438`. Do this for summaries as well as
findings, so the reader can jump directly to the implementation.

For each finding:
- why it matters
- smallest safe change
- whether behavior changes

Then provide a short cleanup plan.

## Questioning Mode

Use this mode when the user wants a question-first review pass before edits.

Goal:
- generate a short markdown file with focused review questions
- each question asks both:
  - what this code means
  - whether this code is necessary

Output file:
- default path: `review_questions_<topic>.md` in workspace root
- keep it short (typically 8-20 questions)

Question format:
- `Q1. [Meaning] What does <code-path/symbol> do in this flow?`
- `Q1. [Necessity] Is <code-path/symbol> necessary, or can it be removed/simplified?`

Prioritize questions around:
- mode/branch conditions
- temporary variables and control flags
- one-line helper functions
- fallback paths and default behavior
- fail-fast vs warn-and-continue decisions
- misleading, ambiguous, or overly complex names

Do not answer the questions in this mode; only generate the question file.

## Commit and Branch-Diff Review

When user asks to review commits or branch differences, use this sequence:

1. Current branch context:
   - `git status`
   - `git log --oneline -n 15`

2. Working tree changes:
   - `git diff --stat`
   - `git diff`

3. Branch comparison (replace `<base>`):
   - `git diff --stat <base>...HEAD`
   - `git diff <base>...HEAD`
   - `git log --oneline <base>..HEAD`

4. Review result format:
   - Findings (severity ordered)
   - Risks/regressions
   - Missing tests
   - Suggested minimal patch set

## Prompt Templates

Use these prompts directly.

### 1) Clean a file

```text
Review @<file> and make it neat and tight.
Constraints:
- Fail fast on invalid states.
- Reduce unnecessary variables/branches.
- Do not over-abstract one-line logic into helpers.
- Keep behavior unchanged unless required for correctness.
Show findings first, then apply minimal edits.
```

### 2) Review staged/unstaged changes

```text
Review current working tree changes with a code-review mindset.
Prioritize: bugs, regressions, hidden behavior changes, missing tests.
Then suggest minimal cleanup for readability and shorter data flow.
```

### 3) Review branch against base

```text
Review this branch against <base> (commit history + full diff).
Check:
- invalid-state handling (fail-fast)
- dead/unused paths
- over-designed abstractions
- unnecessary temporary variables
- duplicated conditional logic
Return findings by severity and a minimal patch plan.
```

### 4) Review specific commit range

```text
Review commits <from>..<to> and summarize:
1) behavior changes
2) potential regressions
3) cleanup opportunities to make code shorter and clearer
4) tests that should be added/updated
```

### 5) Generate question checklist first

```text
Run questioning mode on @<file-or-diff-scope>.
Create a short markdown file named review_questions_<topic>.md.
For each item, ask:
1) what is the meaning/purpose of this code?
2) is it necessary, or can it be removed/simplified?
Do not answer yet; only produce the questions.
```

## Scope Notes

- If unsure whether a path is unused, state uncertainty explicitly and ask before removal.
- Prefer deleting dead code over keeping compatibility shims, unless user requests compatibility.
- Do not mix broad refactors with unrelated style churn.
