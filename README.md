# skills

Agent skills built around the human side of working with AI.

I build and collect skills that fix the daily friction of using coding and personal agents: stripping robotic phrasing out of writing, shaping output for how an ADHD brain actually works, and giving ephemeral agents persistent memory across sessions using plain Markdown and Git.

## Installation

### All agents (OpenCode, Codex, Antigravity, Cursor, Claude Code)

Install all skills:

```bash
npx skills add almahdi/skills
```

Or install a single skill:

```bash
npx skills add almahdi/skills --skill unslop
npx skills add almahdi/skills --skill i-have-adhd
npx skills add almahdi/skills --skill ember
```

### Claude Code marketplace

```text
/plugin install skills@almahdi
```

## Skills

### Writing

- **[unslop](./skills/writing/unslop/SKILL.md)**. Cuts AI tells from any text and adds human voice. Runs automatically on everything the agent writes: docs, code comments, commit messages, PRs, and emails. Adapted from [cursor/plugins](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop).

### Productivity

- **[ember](./skills/productivity/ember/SKILL.md)**. Persistent, repository-backed memory and surgical execution discipline for coding and personal assistants. Keeps `.agent/` and `.memory/` in your repo so your agent remembers state, architectural decisions, and daily sessions without external databases.
- **[i-have-adhd](./skills/productivity/i-have-adhd/SKILL.md)**. Shapes output for a reader with ADHD. Leads with the next concrete action, numbers multi-step work, restates state across turns, suppresses tangents, and makes completed work visible. Adapted from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd).

## How they work

- **`unslop`** is model-invoked. Once installed, it filters every piece of writing the agent produces without needing a command.
- **`ember`** is both model-invoked and command-accessible. It automatically ignites when `.memory/` exists in a workspace, or you can run `/ember init` to bootstrap memory in any repo, `/ember status` to check active work, and `/ember save` to checkpoint a session.
- **`i-have-adhd`** is user-invoked. Activate it with `/i-have-adhd` when you want action-first formatting. It stays on for the rest of the session until you say "stop adhd mode".

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

**Ali Almahdi** ([ali.ac](https://ali.ac) · [@almahdi](https://github.com/almahdi) · [X/@alialmahdi](https://x.com/alialmahdi))
