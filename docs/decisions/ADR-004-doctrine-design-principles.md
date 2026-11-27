---
status: accepted
status-note: ratified by Chris Wells on 2026-11-27
ratified-by: Chris Wells
ratified-on: "2026-11-27"
owner: Chris Wells
kind: design
built: landed
proof: "`AGENTS.md`"
supersedes: nothing
amends: nothing
consulted: Claude, in the brainstorm session that wrote the v0.2 design spec
revisit-when: the v0.3 napkin, written from the family interviews, changes the design principles
---
# ADR-004 — erelong's doctrine is the design spec's eight principles, P1 to P8

## Decision

Every option on erelong is weighed against these eight principles, and the one that serves them best wins:

- **P1 Visible, but limited.** Work stays on screen, and a Today view shows only what matters now.
- **P2 Signal, don't nag.**
- **P3 Everything goes both ways.** Anyone can nudge anyone.
- **P4 Interruptions are rare.** A strict notification budget, with urgent alerts styled differently.
- **P5 Reward right away.** Finishing a card gives an immediate, visible payoff.
- **P6 Plans become actions.** Goals carry if-then plans.
- **P7 Match certainty to time.** Detail for this week, broad themes for next year.
- **P8 API-first.** The project's own clients use only the public API.

They go into the Doctrine section of `AGENTS.md`, which is empty until now.

## Context

- `AGENTS.md` has no doctrine, and says the owner sets one. Chris Wells chose the design spec's principles, each
  with the research behind it (spec §4, lines 63–72; bbq Q8).
- The rationale for each principle, with its sources, stays in the spec (kept out of git, ADR-003).

Drivers:
- agents need a rule for choosing before the build starts
- the principles already carry their research
- the nudge system depends on the notification and reward principles

## Alternatives

### All eight principles (chosen: they already come with research behind them)
- Good: they cover the product's whole stance, from notifications to the API.
- Bad: eight is a lot to weigh at once for a small call.

### A short subset (P2, P3, P8)
- Good: quicker to apply.
- Bad: it drops the notification and reward principles that the nudge system depends on.

### No doctrine yet
- Good: nothing fixed before the family interviews.
- Bad: agents have no rule for choosing until Chris Wells writes one.

## Consequences

- An option that nags, monitors, adds pushes or skips the public API needs a stated reason to win.
- The doctrine can change after the family interviews; that is an amendment or a new ADR.

## History

- 2026-11-27: drafted by makeadr (light route) from Chris Wells's answer to bbq Q8.
- 2026-11-27: ratified by Chris Wells. Earlier values: `status: proposed`; `status-note: drafted 2026-11-27 from the user's answers; awaiting ratification`.
- 2026-11-27: built in `AGENTS.md`. Earlier values: `built: not started`; `proof: queued in this session, after ratification, for the Doctrine section of `AGENTS.md``.
