# almahdi-skills

Agent skills for clear, human writing and engineering.

## Installation

### Claude Code

Install via the Claude Code plugin marketplace:

```
/plugin install almahdi-skills@alialmahdi
```

### OpenCode, Codex, and other agents

```bash
npx skills add alialmahdi/almahdi-skills
```

### Manual

```bash
npx skills add alialmahdi/almahdi-skills --skill unslop
```

## Skills

### Writing

- **[unslop](./skills/writing/unslop/SKILL.md)** — Cut AI tells from any writing. Must always apply to all text the agent produces. Adapted from [cursor/plugins](https://github.com/cursor/plugins/tree/main/pstack/skills/unslop).

### Productivity

- **[i-have-adhd](./skills/productivity/i-have-adhd/SKILL.md)** — Shape output for a reader with ADHD: action-first, numbered steps, no preamble. Adapted from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd).

## Usage

- **`unslop`**: Model-invoked; applies automatically to all writing the agent produces — docs, comments, commit messages, PRs, emails, everything.
- **`i-have-adhd`**: User-invoked; activate with `/i-have-adhd` in chats or clients that support user commands. Stays active until saying "stop adhd mode".

## Development

```bash
# Install dependencies
npm install

# Create a changeset for your change
npx changeset

# Version and publish
npm run version
```
