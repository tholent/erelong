---
status: accepted
status-note: ratified by Chris Wells on 2026-11-27
ratified-by: Chris Wells
ratified-on: "2026-11-27"
owner: Chris Wells
kind: architecture
built: not started
proof: queued for the M0 bbq, run with `napkin` on the v0.3 napkin (`docs/bbq/2026-11-27-napkin-design-spec.md`, Kickoff)
supersedes: nothing
amends: nothing
consulted: Claude, in the brainstorm session that wrote the v0.2 design spec
revisit-when: the v0.3 napkin, written from the family interviews, changes the stack or the milestone plan
---
# ADR-002 — erelong is built new on Python/FastAPI and a SvelteKit PWA, shipped as one Docker image, milestone by milestone

## Decision

erelong is a new codebase, not a fork of an existing kanban app. The backend is Python 3.12+, FastAPI and
Pydantic v2, with SQLAlchemy 2 and Alembic migrations; SQLite (WAL mode) is the default database and PostgreSQL is
optional through `DATABASE_URL`. The client is a SvelteKit PWA on the static adapter that uses only the public
JSON API and is served as static files by FastAPI, so Node is needed at build time only. It ships as one
multi-arch Docker image (`linux/amd64`, `linux/arm64`). The work goes milestone by milestone, M0 to M5 in order,
with M6 (locked boards) optional.

## Context

- Chris Wells kept the stack and the build order as the design spec v0.2 wrote them (bbq record
  `docs/bbq/2026-11-27-napkin-design-spec.md`, Q3 and Q4). The spec is kept out of git (ADR-003); the line numbers
  below are for anyone holding it.
- Backend: spec §9.1 (lines 294–298). Client: §9.2 (line 302). Deployment: §9.4 (line 310). Build vs. fork:
  §10 (lines 325–330). Milestones: §11 (lines 336–344).
- The spec also requires that erelong runs on a Raspberry Pi, a NAS or a VPS from one image (Goals, line 48),
  and that its own client uses only the public API (P8, line 72).
- No build starts before the family interviews (bbq Q5). This ADR fixes the shape the M0 bbq builds on.

Drivers:
- runs on a Pi from one container and one volume
- the client uses only the public JSON API, and works offline in a store
- the nudge and score model is the core and fits no existing data model
- Chris Wells's preference for Python

## Alternatives

### Build new on Python/FastAPI + SvelteKit (chosen: the nudge model fits no existing app, and the stack matches the preference)
- Good: the data model is shaped around cards, weight and score from day one; the backend is one Python process
  on SQLite; the client is static files.
- Bad: every basic kanban feature has to be written, where a fork would have it already.

### Fork Vikunja
- Good: an actively maintained, AGPL kanban and task app.
- Bad: its stack does not match the chosen Python/FastAPI stack (spec line 327).

### Fork Planka or Focalboard
- Good: Trello-like boards already built.
- Bad: Planka is no longer open source; Focalboard's standalone server has gone a long time without a release
  (spec lines 328–329).

### HTMX instead of SvelteKit
- Good: no Node at all, and less client code.
- Bad: it returns server-rendered HTML instead of using the public JSON API, and every tap needs a server round
  trip, which is poor for offline store trips (spec line 302).

## Consequences

- The M0 bbq starts from this stack and does not re-ask it. Folder layout, package tooling and installing Docker
  are its questions (bbq record, Defaulted).
- Docker is not installed on the machine where this was decided (measured 2026-11-27), so M0 needs it first.
- A change of stack after M0 is a new ADR that supersedes this one.

## History

- 2026-11-27: drafted by makeadr (light route) from Chris Wells's answers to bbq Q3 and Q4.
- 2026-11-27: ratified by Chris Wells. Earlier values: `status: proposed`; `status-note: drafted 2026-11-27 from the user's answers; awaiting ratification`.
