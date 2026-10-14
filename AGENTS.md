# AGENTS.md

Knowledge base for creating and maintaining skills in this repo. Read this before creating a new skill or modifying the structure.

## Repo Structure

```
almahdi-skills/
├── .claude-plugin/
│   ├── plugin.json              # Plugin manifest — lists ALL skill paths
│   └── marketplace.json         # Marketplace listing
├── .changeset/                  # Versioning via changesets
├── skills/
│   ├── <bucket>/                # Category: writing, engineering, productivity, etc.
│   │   └── <skill-name>/
│   │       ├── SKILL.md         # The skill (required)
│   │       ├── agents/
│   │       │   └── openai.yaml  # Codex config (only for user-invoked skills)
│   │       └── *.md             # Supporting reference files (optional)
│   └── ...
├── scripts/                     # Build scripts
├── package.json                 # Changesets config
├── AGENTS.md                    # This file
└── README.md
```

## Creating a New Skill

### 1. Choose a bucket

Pick the category that fits:
- `writing/` — writing quality, editing, voice
- `engineering/` — code work, TDD, review, architecture
- `productivity/` — workflow, planning, communication
- `misc/` — rarely used, not promoted

### 2. Create the skill directory and SKILL.md

```
skills/<bucket>/<skill-name>/SKILL.md
```

### 3. Write the SKILL.md frontmatter

```yaml
---
name: skill-name
description: What this skill does. Use when the user wants…, mentions…, asks for…
---
```

**Required fields:**
- `name` — lowercase, hyphens, unique across the repo
- `description` — what it does + trigger phrases for auto-invocation

**Optional fields:**
- `disable-model-invocation: true` — makes it user-invoked only (never auto-invoke)
- `metadata.internal: true` — hides from `npx skills` discovery (only visible with `INSTALL_INTERNAL_SKILLS=1`)

### 4. Write the skill body

Markdown instructions the agent follows when the skill activates. Be specific and actionable. Include:
- What the skill does
- Step-by-step process
- Patterns to detect/fix
- Examples

### 5. Register in plugin.json

Add the skill path to `.claude-plugin/plugin.json`:

```json
{
  "skills": [
    "./skills/writing/unslop",
    "./skills/<bucket>/<new-skill>"
  ]
}
```

## When to Use agents/openai.yaml

Create `skills/<bucket>/<skill-name>/agents/openai.yaml` **only when**:

1. **The skill is user-invoked** (`disable-model-invocation: true`) — add `policy.allow_implicit_invocation: false` so Codex doesn't auto-invoke it:
   ```yaml
   policy:
     allow_implicit_invocation: false
   ```

2. **You want custom Codex UI metadata** — display name and short description:
   ```yaml
   interface:
     display_name: "My Skill"
     short_description: "What it does in one line"
   ```

**Do NOT create openai.yaml for model-invoked skills.** The default behavior (auto-invoke enabled) is what you want.

## Invocation Modes

### Model-invoked (default)

- No `disable-model-invocation` in frontmatter
- No `agents/openai.yaml` needed
- The agent can auto-invoke it based on the description's trigger phrases
- Description should include rich trigger phrasing: "Use when the user wants…, mentions…, asks for…"
- Test: _could the model usefully reach for this autonomously?_

### User-invoked

- Set `disable-model-invocation: true` in frontmatter
- Create `agents/openai.yaml` with `policy.allow_implicit_invocation: false`
- Only reachable when the human types `/skill-name`
- Description should be human-facing, no trigger lists
- A user-invoked skill may invoke model-invoked skills, but never another user-invoked skill

## npx skills Compatibility

The repo works with `npx skills` automatically if:
- Skills are in `skills/<bucket>/<name>/SKILL.md` (up to 3 levels deep)
- Each SKILL.md has valid `name` + `description` frontmatter
- `.claude-plugin/plugin.json` exists and lists all skill paths

Test with:
```bash
npx skills add alialmahdi/almahdi-skills --list
```

## Supporting Files

Skills can have additional `.md` files in their directory for reference material:
```
skills/writing/unslop/
├── SKILL.md
├── patterns.md          # Optional: detailed pattern reference
└── examples.md         # Optional: before/after examples
```

Link to these from the SKILL.md body with relative paths.

## Versioning

Use changesets when adding or modifying skills:
```bash
npx changeset
# describe the change, pick patch/minor/major
```

Then version:
```bash
npm run version
```

## Checklist for New Skills

- [ ] Skill directory created at `skills/<bucket>/<name>/`
- [ ] `SKILL.md` has valid frontmatter (`name`, `description`)
- [ ] `description` includes trigger phrases (if model-invoked)
- [ ] Body is specific, actionable, and well-structured
- [ ] Path added to `.claude-plugin/plugin.json`
- [ ] `agents/openai.yaml` created (if user-invoked)
- [ ] Supporting files added (if needed)
- [ ] Changeset created
