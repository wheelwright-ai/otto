# Seed outline (v0.1 in progress)
- CORE.md: vocabulary, record shapes, Charter Check gate with justification table
- hub/DESIGN.md + hub/steering/{goals,mandates,records,tastes}.md
- skills/ (Agent Skills format): governor, engagement-guide, excavation-migration, lugs, advisors, calibration-survey, sharing-flavors, tread
- scenarios/ (WHEN ... THE HUB SHALL ...; grader/comparator format): the first nine mined from an earlier bootstrap's scars (journal/bootstrap-scars-source.md); evals.json marks release-only checks with cheaper proxies
- journal/: the genesis event log; every incarnation keeps one

## Open items from builder feedback (2026-11-05)
- RESOLVED 2026-11-05: One home for calibration: skills/calibration-survey owns it; START and scenarios/README point there
- RESOLVED 2026-11-05: scenarios/evals.json (17 scenarios, 54 expectations), grader.md, comparator.md in skill-creator format
- RESOLVED 2026-11-05: Costly checks (a never-used home, network off, hour waits) run at release, cheaper proxies per incarnation (see wave 3)
- RESOLVED 2026-11-05: Charter V vs VII split stated in the Charter (0.1.1 PATCH)
- RESOLVED 2026-11-05: Kiro `auto` is real (always, fileMatch, manual, auto; auto needs `name` + `description`, per kiro.dev/docs/steering); `name:` added to goals and records, DESIGN lists all four
- Pinned seed copy: names a commit until the first signed release

## Open items, wave 3 (2026-11-05)
- RESOLVED 2026-11-05: CORE: add `prediction` ledger kind and a `group` glossary entry; calibration-survey writes `prediction` rows
- RESOLVED 2026-11-05: Governor loads at stage 0 (boundaries are written in mandates.md); add pointer in START "Know the words" and fix engagement-guide stage (first meeting: sections 1 to 4; trust earned: 5, 6, 8)
- RESOLVED 2026-11-05: evals.json: mark costly scenarios (001, 003, 011, 014, 015, and 009's second OS) as release-only with cheaper per-incarnation proxies; two tiers in scenarios/README.md
- RESOLVED 2026-11-05: skills/tread (tread.yaml + rendering rule) and skills/sharing-flavors (nomination.yaml) written; every skill listed in llms.txt
- RESOLVED 2026-11-05: hub/DESIGN build task 6 proof: steering files start with front matter, not an inclusion line (all four templates carry `name:` and `description:`)
