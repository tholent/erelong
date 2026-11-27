---
status: accepted
status-note: ratified by Chris Wells on 2026-11-27
ratified-by: Chris Wells
ratified-on: "2026-11-27"
owner: Chris Wells
kind: process
built: landed
proof: "`AGENTS.md`, `CLAUDE.md`, `STATUS.md`, `docs/rules/task-homes.md`, `docs/rules/hot-files.md`, `docs/rules/tool-traps.md`"
supersedes: nothing
amends: nothing
---
# ADR-001 — erelong is set up for agents with pitmaster's conventions: AGENTS.md with all six rule groups, and STATUS.md

## Decision

> 2026-11-27: the ground rule "Work on a branch" this set up is relaxed until v1.0.0 by ADR-005.

erelong uses pitmaster's conventions for working with agents. Every agent reads `AGENTS.md` first in every session
(`CLAUDE.md` is one line, `@AGENTS.md`, so Claude Code loads it too). Its Rules section has all six of pitmaster's
rule groups switched on: plan, run, check, records, plain and craft, 30 rules copied from the catalogue dated
2026-10-23. `STATUS.md` says where the project stands now, and each of its claims cites a file. Chris Wells rules on
taste, naming and direction; agents propose and Chris Wells ratifies. This covers how agents work in the
repository. It does not decide anything about erelong's own code.

## Context

- Agents will do much of the work on erelong, so every session needs to read the same rules and the same record
  of where things stand. The repository is the only memory they share (`AGENTS.md`, Ground rules).
- All six rule groups are on from the start, not just the three pitmaster ticks by default (plan, check, plain).
  Dropping a group later is cheaper than adding habits later. Chris Wells chose this when the project was set up
  on 2026-11-27.
- Only the rules and status pieces were written. The log, debt, archive, glossary, proposals and `pitmaster.md`
  config were left out. This folder was added with this ADR.
- The project has no one-line description and no doctrine (rule for choosing between options) yet. `AGENTS.md`
  says so, and agents do not invent either one.
- Set up with pitmaster project-prep on branch `prep/2026-11-27`, commit faaa7c0.

## Consequences

- Every session pays the context cost of 30 rule lines. That is the price of having all the rules from day one.
- Some rules point at things that do not exist yet. The plain-words rule offers to add terms to a glossary, but
  there is no `docs/glossary.md`. Some craft rules (emulator, hardware, datasheets) only fit if erelong turns out
  to be a hardware or compiled project.
- Turning a rule group off, or adding a missing piece later, is a project-prep run. It changes only the marked
  Rules section of `AGENTS.md`. A change to this decision itself is an amendment or a new ADR.

## Asks left open

1. Should the glossary piece be added so the plain-words glossary rule has a file to use, or that rule dropped?
2. Once erelong's purpose is written down, should any craft rules that do not fit be switched off?

## History

- 2026-11-27: drafted by makeadr (light route) from Chris Wells's answers, right after the project-prep setup.
- 2026-11-27: ratified by Chris Wells. Earlier values: `status: proposed`; `status-note: drafted 2026-11-27 from the user's answers; awaiting ratification`.
- 2026-11-27: amended (see the amendment below), answering the two asks left open. ADR-005 also amends this
  ADR's Decision, relaxing the "Work on a branch" ground rule until v1.0.0.

## Amendment — 2026-11-27, Chris Wells

Touches: Consequences and Asks left open. Agreed by Chris Wells in the napkin bbq
(`docs/bbq/2026-11-27-napkin-design-spec.md`, Q13 and Q14).

1. **Ask 1, the glossary:** add the glossary piece. `docs/glossary.md` starts empty, and terms are filed one at a
   time on Chris Wells's yes, as the plain-words rule says (Q13).
2. **Ask 2, the craft rules:** switch off the two hardware rules, "Name milestones as numbered rungs; reach each
   in the emulator before real hardware." and "Take hardware values and protocol rules from the datasheet or spec
   section, never from memory." The other five craft rules stay on (Q14). The reason: erelong has no hardware.
   It is a web app in Docker, and a Raspberry Pi is only a host. The recommendation to keep all seven was
   overruled.

So the Rules section of `AGENTS.md` holds 28 rules, not 30.
