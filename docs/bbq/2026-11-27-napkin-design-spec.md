# bbq record — erelong from the napkin

2026-11-27 · untyped bbq, seeded by `napkin` · 16 questions · lead: this session (Opus 5.5); no workers

Napkin: `napkins/erelong-design-spec.md` (Design Spec v0.2, 411 lines). It is kept out of git (Q6), so the line
citations below are for anyone holding the file. Its household details (lines 26–37) are deliberately not
repeated here, because this repository is public.

## What this bbq settled

**No build yet.** Work waits until each family member has been interviewed about what they expect (Q5). The
interviews feed a v0.3 napkin, and a fresh napkin bbq on that napkin plans M0.

## Rules from the answers

- **Q1 Count.** 16 questions.
- **Q2 Description.** erelong's one-line public description (proposal from the option chosen; wording is taste,
  yours to change): *"A self-hosted, ADHD-friendly kanban planner for households, with weighted nudges instead of
  nagging."* It goes in `AGENTS.md` and `README.md`, without family details.
- **Q3 Stack.** Keep as written (napkin lines 294–302, 310): Python 3.12+, FastAPI, Pydantic v2, SQLAlchemy 2 +
  Alembic, SQLite (WAL) by default with Postgres optional; SvelteKit static-adapter PWA served by FastAPI, Node at
  build time only; one multi-arch Docker image.
- **Q4 Build order.** Keep as written: build new, not a fork (line 330); milestones M0→M5 in order, M6 optional
  (lines 336–344).
- **Q5 Scope.** "hold off on work until we have an interview with family members regarding expectations." No
  code, scaffolding or build until the interviews are done.
- **Q6 Privacy.** `napkins/` stays out of git (add it to `.gitignore`). Anything taken from a napkin into the
  public repository is rewritten without household or health details.
- **Q7 Landing.** "just work on main for < v1.0.0." Pushing straight to main is approved while the version is
  below v1.0.0. This changes AGENTS.md's ground rule "Work on a branch", which ADR-001 rules: it is an ADR
  candidate (below) and does not change AGENTS.md until that is ruled.
- **Q8 Doctrine.** The napkin's design principles P1–P8 (lines 65–72) are erelong's doctrine: every option is
  weighed against them. P1 visible but limited · P2 signal, don't nag · P3 everything goes both ways · P4
  interruptions are rare · P5 reward right away · P6 plans become actions · P7 match certainty to time · P8
  API-first.
- **Q9 Interview method.** "I will setup a bbq with each family member and walk them through it." Chris runs one
  bbq per member.
- **Q10 Interview topics.** Trello keep/drop (folds in the napkin's open question 1, line 350); what each person
  wants it for; nudges and notifications (feeds the tuning, line 237). Privacy and fairness was offered and **not
  chosen**.
- **Q11 Results.** The interviews are folded, without names, into a v0.3 napkin in the gitignored `napkins/`
  folder. A fresh `napkin` bbq on it plans M0.
- **Q12 v1.0.0.** v1.0.0 is the M5 public release (line 343). Branches and PRs begin there.
- **Q13 Glossary.** Add `docs/glossary.md` (ADR-001 open ask 1), empty to start; terms are filed one at a time,
  on Chris's yes.
- **Q14 Craft rules.** "Switch off the hardware pair" (ADR-001 open ask 2): drop "Name milestones as numbered
  rungs; reach each in the emulator before real hardware" and "Take hardware values and protocol rules from the
  datasheet or spec section, never from memory". Keep the other five craft rules. **Overruled:** the
  recommendation was to keep all seven, reading emulator as arm64 under QEMU/buildx and hardware as the Pi.
- **Q15 Family bbqs.** Free-form each time: Chris steers a plain bbq with each person. Their records go to
  `napkins/interviews/` (out of git), never to `docs/bbq/`.
- **Q16 Anything else to protect or avoid?** Nothing more.

## From the napkins

Cited to `napkins/erelong-design-spec.md`. These were settled without a question, and the build will follow
them unless the v0.3 napkin changes them.

- Self-hosted Docker image first; possible open-source release later; Apache-2.0 (lines 7–8, D3 line 363).
- The API is a first-class product; the project's own web app uses only the public API (lines 22, 72, 256).
- Phone first; respect the teens' autonomy, no monitoring (lines 35–37, 53).
- Non-goals for v1: business features, Gantt dependencies, monitoring, native apps, multi-tenant SaaS, E2EE,
  leaderboards (lines 51–57).
- Everything is a Card; entities as in §5.1 (lines 78–108); card types task, trip and goal (lines 112–116);
  one trip card per store visit, no item catalog in v1 (line 118, D10).
- Views: Today (capped at 7 by default), Board, Trip, Horizons, Year strip (not a Gantt), Calendar with an iCal
  feed (lines 122–129).
- Roles adult | member; minimal adult powers; nobody sees another person's private board or overrides a "Not
  until…"; a member can be promoted to adult (lines 134–143, D6).
- Private boards: no UI or API access for anyone else; honest in-app about the server-admin limit; no E2EE in
  v1; content kept in a replaceable envelope with `content_version`; opt-in locked boards in M6 (lines 146–150,
  D7).
- Nudge weight: exponential decay, stored as `w` and `t_last`, no background job; half-life `H` 4 days
  (lines 162–169).
- Score = `w_now` + deadline pressure; `P_max` 3.0, `LEAD` 7 days; overdue pressure stays capped (lines 174–181).
- Rate limits: 1 per sender per card per 12 h; 5 per sender per recipient per day; 1 urgent per sender per day;
  a calm "already nudged" state, not an error (lines 186–191).
- Urgent toggle only within 24 h of `due_at`, expires at `due_at`, styled differently; Android high-importance
  channel; iPhone plain Web Push (no Time Sensitive); ntfy opt-in, iOS experimental; no native wrapper
  (lines 194–201, D1).
- Recipients see only total weight, never who nudged; `sender_id` never exposed by the UI or any API scope; no
  read receipts or last-seen; weight shown as tiers light → noticeable → heavy → boulder, never as numbers
  (lines 205–208, 274, D4).
- Responses: On it, Need help, Not until…, Done; private celebration; opt-in "share this win"; quiet "a card
  you nudged got done", never a push; no counts or leaderboards (lines 212–224, D5).
- Notification budget: pushes only on a tier crossing, an urgent nudge or a Need help; at most 3 non-urgent
  pushes a day; quiet hours; a daily digest; Declarative Web Push on iOS 18.4+ (lines 227–234).
- All tuning numbers are household settings agreed by the whole family; tuning week after M2 (lines 237, D8).
- Planning: Horizons Now/Next/Later, a why plus if-then plans, progress bars, family language, a yearly review
  template (lines 243–247).
- API: REST + JSON under `/api/v1`; OpenAPI 3.1 at `/api/v1/openapi.json`, docs at `/docs`; contract tests in
  CI; ULIDs, cursor pagination, ETag/If-Match, Idempotency-Key, RFC 9457 errors, ISO 8601 UTC, typed
  `nudge-rate-limited` (lines 254–268).
- Auth: local accounts (password + optional passkey) and scoped PATs in v1; OAuth 2.1 and OIDC later
  (lines 271–273).
- SSE stream; HMAC-SHA256-signed webhooks with retries; the listed event types (lines 277–279); built-in iCal,
  ntfy bridge, quick-add (lines 282–284).
- Backend: in-process scheduler; VAPID keys made on first boot (lines 297–298). Client: guided "Add to Home
  Screen"; offline Today and Trip with queued toggles (lines 303–304).
- Deployment: `ghcr.io/tholent/erelong`, amd64 + arm64; one container, one `/data` volume; env config;
  `docker-compose.yml`; HTTPS required; `/healthz`; a `backup` command (lines 310–314, D11, D12).
- Tooling: ruff, `mypy --strict`, pytest + coverage (≥ 85 % domain, 100 % nudge/score math), pre-commit,
  GitHub Actions, Hypothesis (lines 317–319).
- Open in the napkin and still open: trademark check before public release (line 351); tuning values (line 352);
  ntfy on iOS during M2 (line 353).

## Owed

None.

## Defaulted

- **Lead and workers for the build.** Not asked, since no build is in scope (Q5); the bbq on the v0.3 napkin asks
  it, with `tier-select`. veto: name a lead now.
- **Docker.** Docker is not installed on this machine (measured 2026-11-27: `docker --version` → command not
  found). Python 3.13.5, uv 0.13.9 and Node 20.19.2 are installed. Installing Docker is left for the M0 bbq.
  veto: say to install it now.
- **Folder layout and package tooling** (uv or pip, `backend/` + `web/`). Not in the napkin; the M0 bbq asks it.
  veto: rule it now.
- **Feature flags.** The craft rule "Land a new feature switched off behind a flag … until the owner approves
  how it looks" stays on; how it applies is the M0 bbq's question. veto: say how now.
- **PR #1.** The prep branch's PR #1 (project-prep + ADR-001) is still open; main holds only the initial commit
  (`git log origin/main`). It merges before anything is pushed to main under Q7. veto: keep it open.

## ADR candidates

- **Q3 + Q4 Stack and build-new.** Signs: chose between options with merit (HTMX, forks); fixes what all later
  work builds on.
- **Q6 Napkins stay out of git.** Signs: a standing "never" rule for a public repository.
- **Q7 + Q12 Work on main below v1.0.0.** Signs: a standing rule; it narrows AGENTS.md's "Work on a branch",
  which ADR-001 rules; it overrules the recommendation (a PR for each rung).
- **Q8 P1–P8 as doctrine.** Signs: a standing rule for choosing; it fills AGENTS.md's Doctrine section.
- **Q13 + Q14 ADR-001's two open asks** (add the glossary; switch off the hardware pair). Signs: touches an
  existing ADR; Q14 overrules the recommendation. An amendment to ADR-001.

## Kickoff

Now, in this session: merge PR #1; ignore `napkins/` in `.gitignore`; rule the ADR candidates with `makeadr`;
then make the changes they allow (the description, the doctrine, the main-branch rule, the glossary, the craft
rules) in `AGENTS.md`, `README.md` and `STATUS.md`, and push to main.

Later, once Chris has run the family bbqs and written the v0.3 napkin:

> Run `napkin` on erelong's v0.3 napkin, grounded in `docs/bbq/2026-11-27-napkin-design-spec.md`, to plan M0.
> Lead: Opus 5.5 at the effort that bbq picks with `tier-select`. A session on another model must stop and say
> so before doing anything.
