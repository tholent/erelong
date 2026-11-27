---
status: accepted
status-note: ratified by Chris Wells on 2026-11-27
ratified-by: Chris Wells
ratified-on: "2026-11-27"
owner: Chris Wells
kind: process
built: landed
proof: "`AGENTS.md`"
supersedes: nothing
amends: ADR-001 §Decision (the Ground rules it set up in `AGENTS.md`)
revisit-when: erelong reaches v1.0.0, the M5 public release
---
# ADR-005 — Until v1.0.0, agents work and push straight on main; branches and PRs begin at the M5 public release

## Decision

While erelong's version is below v1.0.0, agents may commit and push straight to `main` without asking each time.
v1.0.0 is the M5 public release. From then on, work goes on a branch and lands by PR, and `AGENTS.md`'s ground
rule "Work on a branch. Never push straight to the main branch without Chris Wells's approval." applies again in
full. This replaces only that ground rule, and only until v1.0.0.

## Context

- Chris Wells: "just work on main for < v1.0.0" (bbq Q7), and v1.0.0 is the M5 public release (bbq Q12; spec
  §11, line 343).
- The reason: until the public release, only Chris Wells and the family use erelong. PR review would add waiting
  without catching much, and main can be fixed forward.
- `AGENTS.md`'s Ground rules, set up under ADR-001, say to work on a branch. This ADR is the standing approval
  that rule asks for.

Drivers:
- only Chris Wells and the family use erelong before M5
- no CI exists yet
- review should start when outsiders self-host

## Alternatives

### Work on main below v1.0.0 (chosen: no outside users yet)
- Good: no waiting on a merge for each change.
- Bad: nothing is reviewed before it reaches main, and a bad push is fixed forward.

### A PR for each rung, merged by Chris Wells (overruled)
- Good: Chris Wells sees each rung before it lands.
- Bad: every rung waits on a merge.

### Merge on green
- Good: fast, with CI as the gate.
- Bad: needs CI before there is any, and Chris Wells sees the work only after it lands.

## Consequences

- Each push to main is still reported with its commit, and the content proven at the destination (`AGENTS.md`,
  Records rule).
- At v1.0.0 a session switches the ground rule back. It does not need a new ADR, because this one already says
  when it ends.

## History

- 2026-11-27: drafted by makeadr (light route) from Chris Wells's answers to bbq Q7 and Q12. ADR-001 gets a
  History note pointing here, in the same commit.
- 2026-11-27: ratified by Chris Wells. Earlier values: `status: proposed`; `status-note: drafted 2026-11-27 from the user's answers; awaiting ratification`.
- 2026-11-27: built in `AGENTS.md`. Earlier values: `built: not started`; `proof: queued in this session, after ratification, for the Ground rules of `AGENTS.md``.
