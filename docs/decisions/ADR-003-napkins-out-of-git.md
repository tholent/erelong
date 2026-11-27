---
status: accepted
status-note: ratified by Chris Wells on 2026-11-27
ratified-by: Chris Wells
ratified-on: "2026-11-27"
owner: Chris Wells
kind: process
built: landed
proof: "`.gitignore`"
supersedes: nothing
amends: nothing
---
# ADR-003 — Napkins and family interview records stay out of git, and nothing personal from them enters the public repository

## Decision

The `napkins/` folder is never committed: `.gitignore` lists it. That covers the design spec and the family
interview records in `napkins/interviews/`. Anything taken from a napkin into the repository (a record, an ADR, a
README line) is rewritten without household or health details, and cites napkin lines rather than quoting
private ones.

## Context

- `tholent/erelong` is a public repository (measured 2026-11-27 with `gh api repos/tholent/erelong`:
  `private: false`).
- The design spec v0.2 in `napkins/` describes the household in personal detail in its §2
  (lines 26–37).
- Chris Wells chose to keep it out of git so that nothing private gets published (bbq Q6). The family interview
  records go to `napkins/interviews/`, never `docs/bbq/` (bbq Q11 and Q15).

Drivers:
- the repository is public
- the spec holds personal household details
- agents still need to cite the spec

## Alternatives

### Keep napkins out of git (chosen: nothing private gets published)
- Good: the public repository holds no family details, and the line citations still work for anyone holding the
  file.
- Bad: an agent on another machine or in a cloud session cannot read the napkin from git; it has to be handed
  the file.

### Commit it as is
- Good: the simplest, and every session can read it from git.
- Bad: it publishes the personal household details.

### Make the repository private
- Good: everything can be committed freely now.
- Bad: the history would need cleaning before going public at M5, and a slip would publish it all at once.

## Consequences

- A session that needs the napkin needs a copy of `napkins/` from Chris Wells.
- Every record and ADR drawn from a napkin is checked for private details before it is committed.

## History

- 2026-11-27: drafted by makeadr (light route) from Chris Wells's answer to bbq Q6. The `.gitignore` line
  landed in commit 604925b, the same session.
- 2026-11-27: ratified by Chris Wells. Earlier values: `status: proposed`; `status-note: drafted 2026-11-27 from the user's answers; awaiting ratification`.
- 2026-11-27: three lines in Context and Alternatives reworded to say less about the household, under this ADR's own rule; the meaning is unchanged. Earlier wording is in commit 8463644.
