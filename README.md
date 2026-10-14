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

- **[unslop](./skills/writing/unslop/SKILL.md)** — Cut AI tells from any writing. Must always apply to all text the agent produces.

## Usage

Once installed, the `unslop` skill is model-invoked and applies automatically to all writing the agent produces — docs, comments, commit messages, PRs, emails, everything.

## Development

```bash
# Install dependencies
npm install

# Create a changeset for your change
npx changeset

# Version and publish
npm run version
```
