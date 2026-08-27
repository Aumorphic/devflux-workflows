# DevFlux — Structured Workflows for Claude Code, Cursor & Windsurf

Six markdown files that turn a slash command into a step-by-step process — so your AI coding assistant investigates before it edits, and verifies before it declares a task done.

Built primarily for **Claude Code**, and works the same way in **Cursor** and **Windsurf**, since all three read plain markdown as custom commands.

→ Full product & purchase: [devflux.pro](https://devflux.pro)

---

## The problem this solves

Ask an AI coding assistant to "fix this bug," and most of the time it skips straight to writing code — no reading the surrounding context, no checking who else calls the function it's about to change, no verifying the fix didn't break something else. That's how a 10-minute bug fix turns into three broken files and fifteen re-prompts.

Rules files (`.cursorrules`, `CLAUDE.md`) fix *what the AI knows* about your project. They don't fix *what steps it takes* on a given task. DevFlux is the second piece — a set of structured, on-demand processes for the moments that cause the most damage.

## The 6 workflows

| Command | For | What it forces |
|---|---|---|
| `/fix-known-bug` | A bug you can already describe | Gathers full context first, proposes a fix (root cause, file, lines, risk) and stops for your approval before touching code, then verifies the implementation matches the proposal line-by-line |
| `/investigate-complex-bug` | A bug with no obvious cause | Reproduce it, form multiple ranked hypotheses, test before fixing — not guess-and-check |
| `/build-feature` | A new feature | Study existing patterns before writing new code, so it matches your architecture |
| `/large-refactor` | Changes spanning many files | Map dependencies first, then proceed file-by-file with verification at each step |
| `/add-test-coverage` | Writing tests | Analyze real code paths and edge cases before generating test code, not just happy-path boilerplate |
| `/fix-regression` | A dependency upgrade broke something | Check the changelog for what actually changed, before touching your code |

**`fix-known-bug.md` is included in full in this repo** — see [`workflows/fix-known-bug.md`](./workflows/fix-known-bug.md). The remaining five ship with the full product at [devflux.pro](https://devflux.pro).

## Installation

Copy workflow files into the folder your tool reads for custom commands.

**Claude Code**
```
.claude/commands/
```
(Claude Code also supports the newer `.claude/skills/` format — files in `.claude/commands/` still work and are the simpler starting point.)

**Cursor**
```
.cursor/commands/
```

**Windsurf**
```
~/.windsurf/workflows/
```
Note: this is a global, per-user folder, not per-project — workflows placed here apply across all your Windsurf projects.

Then type `/` in your AI chat. The command should appear in the autocomplete list.

```
/fix-known-bug
The login endpoint throws a 500 error when the email field contains a plus sign.
```

Full setup walkthrough, including common mistakes: [`docs/installation.md`](./docs/installation.md).

## Why markdown, not a plugin

No dependencies, no API keys, nothing to update. A workflow file can't break when an editor updates its internals, can't phone home, and can't drift out of sync with what you think it's doing — you can open it and read every instruction it gives the model. Moving from one tool to another is a matter of changing which folder the file lives in, not rewriting anything.

Longer version: [`docs/how-workflows-work.md`](./docs/how-workflows-work.md).

## FAQ

**Do I still need a `.cursorrules` / `CLAUDE.md` file?**
Yes — keep it. Rules files handle passive context (your stack, conventions, style). Workflows handle active process during a specific task. They're complementary, not a replacement for each other.

**Can I edit the workflow files?**
Yes, they're plain text. Nothing about using DevFlux prevents you from adjusting the wording to fit your project.

**Does it work in a monorepo?**
Yes — since it's just markdown read by your tool's existing folder structure, repo size and layout don't matter.

Full FAQ: [`docs/faq.md`](./docs/faq.md).

## Related reading

- [DevFlux vs. cursor.directory](https://devflux.pro) — free rules vs. a structured process
- [DevFlux vs. claude-code-workflows](https://devflux.pro) — 6 files vs. a full multi-agent pipeline

## License

The workflow file in this repo (`workflows/fix-known-bug.md`) is provided as a free sample. See [devflux.pro](https://devflux.pro) for the full set and terms.
