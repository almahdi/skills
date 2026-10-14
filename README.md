# Ali Almahdi's Agent Skills

[![skills.sh](https://skills.sh/b/almahdi/skills)](https://skills.sh/almahdi/skills)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Practical skills for how I actually work with AI every day.**

Out of the box, AI agents have three annoying habits. They write in stiff corporate clichés, they bury a ten-second command under three paragraphs of polite preamble, and they forget everything the moment you close the terminal.

I have been building software and systems since 1999. These are the skills I use every day to make coding and personal agents fit how humans actually think, read, and work. They are small, plain Markdown, and work with any model or harness.

Take them, hack on them, and make them your own.

## Installation

Pick one method per agent so you do not install duplicate skills.

### Via `npx skills` (OpenCode, Codex, Antigravity, Cursor, Claude Code)

Install the full collection:

```bash
npx skills add almahdi/skills
```

Or install individual skills:

```bash
npx skills add almahdi/skills --skill unslop
npx skills add almahdi/skills --skill ember
npx skills add almahdi/skills --skill i-have-adhd
```

### Via Claude Code plugin marketplace

```text
/plugin install skills@almahdi
```

## What is inside

### Writing

- **[unslop](./skills/writing/unslop/SKILL.md)**. Strips AI tells from any text and puts a real human voice back in. It runs automatically on everything the agent writes: docs, code comments, commit messages, PRs, and emails. Adapted from [cursor/plugins](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop).

### Productivity

- **[ember](./skills/productivity/ember/SKILL.md)**. Persistent, repository-backed memory and surgical execution discipline for coding and personal assistants. It maintains `.agent/` and `.memory/` inside your repo so your assistant tracks active work, architectural decisions, and daily sessions using plain Markdown and Git.
- **[i-have-adhd](./skills/productivity/i-have-adhd/SKILL.md)**. Shapes output so an ADHD brain can act on it immediately. First line is the action. Multi-step work is numbered. State is restated every turn. Tangents are suppressed, and wins are visible. Adapted from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd).

## How they run

| Skill | Trigger | How to use |
| :--- | :--- | :--- |
| **[`unslop`](./skills/writing/unslop/SKILL.md)** | Automatic (model-invoked) | Always active on all text output. No command needed. |
| **[`ember`](./skills/productivity/ember/SKILL.md)** | Automatic + `/ember` | Auto-ignites when `.memory/` exists. Run `/ember init` to bootstrap a repo, `/ember status` to check active work, or `/ember save` to checkpoint. |
| **[`i-have-adhd`](./skills/productivity/i-have-adhd/SKILL.md)** | Manual (`/i-have-adhd`) | Type `/i-have-adhd` to turn on action-first mode for the session. Say `"stop adhd mode"` to turn it off. |

## Development

```bash
# Install dependencies
npm install

# Create a changeset for your change
npx changeset

# Version and sync plugin manifest
npm run version
```

## Author

**Ali Almahdi** · [ali.ac](https://ali.ac) · [GitHub (@almahdi)](https://github.com/almahdi) · [X (@alialmahdi)](https://x.com/alialmahdi)
