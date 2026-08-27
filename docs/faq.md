# FAQ

**What exactly is DevFlux?**
A set of markdown workflow files that turn a slash command in your AI coding assistant into a structured, step-by-step process for a specific task — fixing bugs, building features, refactoring, testing, and handling dependency upgrades — instead of a free-form prompt.

**Which tools does it work with?**
Built primarily for Claude Code. Works the same way in Cursor and Windsurf, and in principle any tool that reads markdown files as custom commands.

**Is it a plugin or extension?**
No. It's plain markdown files placed in a folder your tool already reads natively. Nothing to install beyond copying files.

**Do I need an API key?**
No. It uses your existing AI coding assistant's own model access — DevFlux makes no separate API calls of its own.

**Do I still need a `.cursorrules` or `CLAUDE.md` file?**
Yes, and you should keep it. Rules files handle passive context (your stack, conventions, style). Workflows handle active process during a specific task. They work together, not instead of each other.

**Can I customize the workflows?**
Yes. They're plain text, so you can open and edit any of them to better match your project or team's conventions.

**Will it work with a monorepo?**
Yes — since it's just markdown read by the tool's existing folder structure, it works the same way regardless of repo size or structure.

**Does it require a specific programming language or framework?**
No. The workflows describe a general process (investigate, plan, implement, verify) rather than language-specific rules, so they apply across stacks.

**What happens if my tool updates its command system?**
Because the files are just markdown, they're insulated from most internal API changes. As long as the tool still reads a folder of `.md` files for custom commands, the workflows keep working.

**Can I use it on a team?**
Yes — since the files are just text, you can commit them to your repository (for project-scoped folders like Claude Code's or Cursor's) so every team member gets the same commands automatically.

**How is this different from just writing a good prompt?**
A prompt is a one-off instruction you have to recreate each time. A workflow file encodes the same discipline permanently, so it applies consistently without you having to remember the right phrasing on every task.

**Where can I get the other five workflows?**
The full set — `investigate-complex-bug`, `build-feature`, `large-refactor`, `add-test-coverage`, and `fix-regression` — ships with the product at [devflux.pro](https://devflux.pro). This repo includes `fix-known-bug` in full as a free sample.
