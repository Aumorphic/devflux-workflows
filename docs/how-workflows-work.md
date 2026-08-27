# How a Workflow File Actually Works

A DevFlux workflow file is plain markdown — no proprietary syntax, no compiler, nothing hidden. Every major AI coding tool already knows how to read a markdown file as instructions when you trigger it with a slash command; DevFlux doesn't add a new mechanism, it just uses that existing one deliberately.

## It's a sequence, not a prompt

The core difference between a workflow file and a regular prompt is structure. A prompt is usually one block of instructions. A workflow file is broken into explicit, ordered phases the AI has to work through:

1. **Context-gathering instructions** — what to read, and in what order, before forming any opinion about the problem.
2. **Analysis instructions** — how to reason about what's happening, often explicitly requiring multiple candidate explanations rather than the first one that comes to mind.
3. **Action instructions** — what kind of change is appropriate, and what's explicitly out of scope.
4. **Verification instructions** — what has to be checked before the task counts as done.

See [`workflows/fix-known-bug.md`](../workflows/fix-known-bug.md) in this repo for a real example of this structure.

## Triggered, not passive

Unlike a `.cursorrules` or `CLAUDE.md` file — which gets loaded automatically at the start of a session or on every matching file — a workflow file only enters context when you explicitly invoke its slash command. This matters for two reasons:

- **Cost.** A workflow doesn't tax every unrelated turn in a session the way an always-on rule would.
- **Consistency over long sessions.** Because it's re-injected fresh at the moment you invoke it, a workflow run two hours into a session gets the same full-strength instructions as one run at the start — it isn't relying on something stated at the beginning of the conversation still carrying weight after a long back-and-forth.

## Why this generalizes across tools

Because it's just markdown describing a process, the same file works whether it's triggered by Claude Code's slash commands, Cursor's command system, or Windsurf's workflow folder — only the folder it lives in changes. The instructions themselves don't need to be rewritten per tool, which is why the same six files work across all three without a "ported" version for each.

## Why not a plugin

A plugin or extension is code running inside your editor with some level of access to your project and, sometimes, your network. A markdown file is inert text — it can't execute code, phone home, or change behavior without you explicitly editing it. It also can't break when an editor updates its internal APIs, because there's no API surface to break: as long as the tool can read a folder of `.md` files and respond to a slash command, the workflow keeps working.
