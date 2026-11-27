# STATUS — erelong

_Last updated: 2026-11-27_

The project's live state. Update it when work lands. Every claim cites at least one file that exists.

## Now

- Design settled, nothing built: the stack and the build order are ruled in ADR-002
  (`docs/decisions/ADR-002-stack-and-build-new.md`), and the doctrine P1–P8 in ADR-004 (`AGENTS.md`, Doctrine).
- No build starts before the family interviews (`docs/bbq/2026-11-27-napkin-design-spec.md`, Q5).
- Work goes straight on main until v1.0.0 (`docs/decisions/ADR-005-work-on-main-below-v1.md`).
- The design spec lives in `napkins/`, out of git, since this repository is public (`.gitignore`,
  `docs/decisions/ADR-003-napkins-out-of-git.md`).

## Next

- Chris Wells runs a free-form bbq with each family member on Trello keep/drop, what each wants it for, and nudges
  and notifications. The records go to `napkins/interviews/` (`docs/bbq/2026-11-27-napkin-design-spec.md`, Q9–Q11, Q15).
- Fold the interviews into a v0.3 napkin, then run `napkin` on it to plan M0 (`docs/bbq/2026-11-27-napkin-design-spec.md`, Kickoff).

## Known debt

- Docker is not installed on the dev machine, and M0 needs it (measured 2026-11-27; `docs/decisions/ADR-002-stack-and-build-new.md`, Consequences).
- The two hardware craft rules were removed by hand inside the project-prep block, so a later project-prep run
  could put them back; check `AGENTS.md` after one (`docs/decisions/ADR-001-pitmaster-conventions.md`, Amendment).

## Log

- 2026-11-27: napkin bbq on the v0.2 design spec (`docs/bbq/2026-11-27-napkin-design-spec.md`); PR #1 merged;
  ADR-002 to ADR-005 drafted and ratified; ADR-001 amended (glossary added, `docs/glossary.md`; hardware craft rules off).
- 2026-11-27: prepared with project-prep; ADR-001 drafted with makeadr and ratified.

## How this file is kept

Live state stays here: what works now, what is next, and the top of the debt list. Every bullet under Now, Next
and Known debt cites at least one file that exists. Keep this file under 300 lines; the project-prep
skill's `scripts/status-check.py` checks both.
