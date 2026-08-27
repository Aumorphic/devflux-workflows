# How a Workflow File Actually Works

A DevFlux workflow file is plain markdown — no proprietary syntax, no compiler, nothing hidden. Every major AI coding tool already knows how to read a markdown file as instructions when you trigger it with a slash command; DevFlux doesn't add a new mechanism, it just uses that existing one deliberately, with real structure behind it.

## A real example: `/fix-known-bug`

Rather than describe this abstractly, here's the actual shape of the included workflow ([`workflows/fix-known-bug.md`](../workflows/fix-known-bug.md)):

1. **Gather context — and stop.** Before any code is touched, the workflow requires the AI to ask you what the issue actually is (expected vs. actual behavior, reproduction steps, suspected area, recent changes) and explicitly waits for your answer rather than guessing.
2. **Propose, don't implement.** The AI reads the relevant code, identifies a root cause, and outputs a structured proposal — issue, root cause, file, exact change needed, lines affected, risk. No code is written yet.
3. **Stop again for approval.** The proposal is presented and the workflow waits for you to approve or ask for a revision before any file is touched.
4. **Implement exactly what was approved.** Only the specific proposed lines change. Any deviation has to be flagged, not silently included. Tests are added or updated for the modified code as part of this step.
5. **Verify against the original proposal**, line by line — not just "does it look right," but an explicit comparison between what was proposed in step 2 and what actually landed in the diff, with deviations reported.
6. **Hand off to test coverage.** The workflow finishes by explicitly invoking a separate test-writing workflow with the relevant context, rather than treating testing as an afterthought.

Every step re-states the issue in one line before doing any work — a deliberate anti-drift measure, so the AI can't lose track of what it's solving partway through a longer task.

## Why this structure, not just a prompt

The pattern above — gather context, propose, get approval, implement exactly what was approved, verify against the proposal — is close to how a careful engineer would actually work with a reviewer, compressed into a single markdown file instead of a multi-person process. A free-form prompt can ask for the same care, but nothing forces the AI to actually stop and wait for your input at the right moments, or to hold itself to a written proposal rather than improvising during implementation.

## Triggered, not passive

Unlike a `.cursorrules` or `CLAUDE.md` file — loaded automatically at the start of a session or on every matching file — a workflow file only enters context when you explicitly invoke its slash command. Because it's re-injected fresh at the moment you invoke it, a workflow run two hours into a session gets the same full-strength instructions as one run at the start.

## Why this generalizes across tools

Because it's just markdown describing a process, the same file works whether it's triggered by Claude Code's slash commands, Cursor's command system, or Windsurf's workflow folder — only the folder it lives in changes. The instructions themselves don't need to be rewritten per tool.

## Why not a plugin

A plugin or extension is code running inside your editor with some level of access to your project and, sometimes, your network. A markdown file is inert text — it can't execute code, phone home, or change behavior without you explicitly editing it. It also can't break when an editor updates its internal APIs, because there's no API surface to break.
