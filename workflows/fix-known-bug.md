---
description: Fix a bug you can already describe (you have an error message, a stack trace, or a clear description of broken behavior) with a minimal, verified change.
---

# Fix Known Bug

Use this workflow when you already know roughly what's wrong — you have an error message, a stack trace, or a clear description of broken behavior. Do not write or edit any code until Step 1 and Step 2 are complete.

## Step 1: Understand the problem before touching code

- Read the reported error or behavior carefully. Identify the exact file(s) and line(s) involved.
- Read the surrounding code — not just the failing line. Read the full function, and identify anything else in the file or codebase that calls it or depends on its current behavior.
- Do not propose a fix yet. State in one or two sentences what you now understand about the cause.

## Step 2: Confirm the intended behavior

- Identify what the code was *supposed* to do, based on naming, comments, tests, and surrounding usage — not just what it's currently doing.
- Note any other code paths that rely on the current (buggy) behavior. A fix that resolves the reported symptom but breaks a dependent code path is not an acceptable fix.
- If the intended behavior is ambiguous, ask a clarifying question rather than guessing.

## Step 3: Apply a minimal, targeted fix

- Make the smallest change that resolves the confirmed root cause.
- Do not perform unrelated refactoring, renaming, or "cleanup" in the same change.
- If the true fix requires a broader change than expected, say so explicitly and explain why, rather than silently expanding scope.

## Step 4: Verify

- Confirm the original reported issue is actually resolved.
- Check the callers and dependent code paths identified in Step 1 — confirm none of them now behave unexpectedly.
- If tests exist for this code, run them. If no test exists for this exact bug, note that as a gap (consider `/add-test-coverage` separately) rather than silently skipping verification.
- Summarize: what was wrong, what changed, and what you verified.

---

*Part of [DevFlux](https://devflux.pro) — structured workflows for Claude Code, Cursor, and Windsurf.*
