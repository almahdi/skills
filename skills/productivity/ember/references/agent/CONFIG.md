# Configuration

Repository-level settings for Ember. Explicit operator instructions and
higher-priority policies take precedence.

## Memory

- Backend: Git-tracked Markdown
- Active: true
- Auto-log: true
- Retrieval order: relevance first, recency second
- Active-memory file: .memory/ACTIVE.md
- Memory index: .memory/INDEX.md
- Redact secrets: true
- Store hidden reasoning: false

## Persistence

- Create commits automatically: false
- Push automatically: false
- Deploy automatically: false
- Publish automatically: false

## Execution

- Verify remembered facts before consequential use: true
- Require observable success criteria for non-trivial work: true
- Preserve unrelated files and changes: true
- Prefer the smallest complete implementation: true

Change these defaults only when the operator establishes a durable repository
preference. A one-off authorization does not automatically update this file.
