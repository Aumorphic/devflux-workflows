# Installation

Setup is identical in spirit across all three tools: copy markdown files into the folder your tool reads for custom commands.

## Claude Code

```
.claude/commands/
```

Place workflow files in this folder inside your project root. Claude Code also supports the newer `.claude/skills/` format — command-style files in `.claude/commands/` continue to work and are the simpler starting point if you're just getting started.

## Cursor

```
.cursor/commands/
```

Same pattern — project-level folder. If it doesn't exist yet, create it.

## Windsurf

```
~/.windsurf/workflows/
```

This is a **global** folder in your home directory, not per-project — workflows placed here become available across all your Windsurf projects at once.

## Verifying it loaded

Open your AI chat panel and type `/`. The workflow should appear in the autocomplete list (e.g. `/fix-known-bug`). If it doesn't appear, this is almost always a folder-location issue rather than a content issue — double check the path above for your tool.

## Using it

Type the slash command, then describe the task in a sentence or two. The workflow file supplies the structure; you supply the specifics.

```
/fix-known-bug
The login endpoint throws a 500 error when the email field contains a plus sign.
```

## Common setup mistakes

- **Wrong folder scope.** Claude Code and Cursor commands are typically project-level; Windsurf's workflow folder is global. Putting a Windsurf-style file in a project folder (or vice versa) means it won't be found.
- **File extension issues.** Keep files as `.md` — renaming or converting them can break how the tool parses them.
- **Expecting automatic loading.** Unlike a rules file, workflows aren't loaded passively into every conversation. You have to actively invoke them with the slash command for that specific task.

## Using across multiple tools

Because the underlying files are the same regardless of which tool reads them, if your team uses more than one AI coding tool, you can maintain a single source copy and place it in each tool's respective folder — keeping the process consistent no matter which tool a given teammate prefers.
