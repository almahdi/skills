# Memory index

Use this file to locate durable context. Retrieve only entries relevant to the
current request, then verify consequential facts against the current system.

## Always read

- `ACTIVE.md` — current objectives, blockers, and exact resumption points

## On demand

- `state/` — current verified facts about architecture, environment, commands,
  dependencies, conventions, and integrations (mutable)
- `decisions/` — consequential choices and rationale in ADR format
- `sessions/` — dated, append-only records of meaningful working sessions (`YYYY-MM-DD.md`)

## Entry conventions

State entries should include the fact, status, source when available, observation
date (`Updated: YYYY-MM-DD`), and confidence when useful.

Decision entries (`decisions/NNN-title.md`) should include context, decision,
alternatives, rationale, consequences, date, status, and any superseded record.

Session filenames use `YYYY-MM-DD.md`. Do not create empty directories or
placeholder entries; add each memory category only when real information exists.
