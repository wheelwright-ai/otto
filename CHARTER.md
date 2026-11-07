<!--
Sync Impact (1.1.2)
- 1.1.1 -> 1.1.2 PATCH: wording only, no principle added, removed or redefined. II now says how the shell grows: prove the smallest thing fast before scaling; no new capability is added while the open chamber's seal is unproven (the operator's words: "test and prove fast before scaling"). Raw environment, applying IV's "survey before changing": every wheel session runs in the agent's raw mode, and the first cut surveys the user's global installs as `foreign` findings and changes nothing (START First cut, CHAMBERS.md chamber 0, SMOKE S-0-06 step 2). WORK.md allows an optional `usage` field (tokens, or `null`) on plan, execute and verdict rows. Deferred until chamber 0 seals: a usage smoke check, a board Cost line, and specialists in the hub.
- Exempt from the failing-check rule (Governance: PATCH). Evidence anyway: the first chamber-0 seal test ran S-0-07 red at end on logs a global agent hook wrote into the wheel (seal-test wheel rows r-000028, r-000042, r-000044); raw mode removes the cause instead of recording around it.
- Measure: S-0-07 at the next chamber-0 seal test. Baseline: red at end.

Sync Impact (1.1.1)
- 1.1.0 -> 1.1.1 PATCH: wording only, no principle added, removed or redefined. SMOKE S-0-07 now names foreign files (written by another tool on the machine): recorded as `foreign` rows, excluded from tracking only after the user's yes, never deleted without one; the interview asks once (GOALS.md). S-0-05 describes absolute-path patterns in words, not as literals. S-0-04 and S-0-08 allow `not_run` "no board yet" only before cut 1's first step 08. WORK.md: a blocked verifier prints its verdict row and the executor appends it with `appended_by`; a `fast` builder that plans its own items records `planner_lane: fast`. START step 03 names the planner lane. BOARD.md's Work section lists every verdict row per item.
- Exempt from the failing-check rule (Governance: PATCH). Evidence anyway: the first chamber-0 seal test on a `fast`-lane build. S-0-05 ran red at cut 1 start on the seed's own pattern text (seal-test row r-000017); S-0-07 ran pass at start and red at end on hook-written logs, with no wording that let it pass once recorded (r-000028, r-000042, r-000044); S-0-04 had no rule for a missing board and the builder improvised `not_run` (r-000016), while S-0-08's rule keyed on the seal rather than step 08; the stand-in's board review found the Work section showed no verdicts, so two fail verdicts were invisible (r-000045). The builder correctly refused to seal cut 1 and opened cut 2.
- Measure: the next chamber-0 seal test. Baseline: cut 1 unsealed, S-0-07 red at end.

Sync Impact (1.1.0)
- 1.0.0 -> 1.1.0 MINOR: IX widened from "per-user taste, default plain" to "per-user taste and crafted": what the user sees is designed for their goals and taste with advanced, effective design craft, never a generic template; plain only until the interview records their taste. The first cut now opens with the specialist interview (GOALS.md): goals, direction, budget, how the user wants to see progress, and presentation taste.
- Failing check: the operator's feedback that every solution so far looks alike and that the first sprint board was "not clear what is being conveyed"; in the v0.1 trials boards were rebuilt three times before they read clearly. No check recorded the user's taste or proved the board followed it.
- Measure: new smoke S-0-08 (the latest taste row id appears in the board's stamp line), and each chamber's seal now includes the user's review of that chamber's board against their taste (CHAMBERS.md). Baseline: null (no taste check existed).

Sync Impact (1.0.0)
- 0.3.0 -> 1.0.0 MAJOR: a restart. Principles regrouped under three new ones (I to III); v0.1 sealed in archive/v0.1/.
- Failing check: the v0.1 proof board (journal/PROOF-BOARD.md, journal/levers.md). Over four graded rounds the seed grew while scores stayed at 5 to 10 of 17 or 18 scenarios; the smaller model trailed the larger in every comparable round (6 vs 8, 7 vs 10, 5 vs 8); every builder forecast ran 6 to 11 high. No check proved that what held at a cut's start still held at its end.
- Measure: the chamber 0 seal (CHAMBERS.md), graded on a fast-lane build. Baseline: none sealed.
- "Cut" now means one pass of the START.md loop, not a factory release.
-->
# Wheelwright Charter

Wheelwright grows a user's AI-work setup the way a nautilus grows its shell: one chamber at a time, each sealed behind it, all on one spiral driven by the user's goals.

**Mission:** recursive self-improvement, in a transparent and collaborative way.

## I. Goals are the alignment
Every cut MUST start from the user's current goals (GOALS.md). Every work item MUST trace to an active goal and name the measure it moves. Adding, revising or dropping a goal is a normal event: versioned, with its reason and the user's words. When work and goals disagree, the goals win.

## II. Grow the shell
The wheel grows chamber by chamber (CHAMBERS.md), one open at a time. A chamber is sealed only when a non-builder proves its seal condition and the board shows it. Prove the smallest thing fast before scaling: no new capability is added while the open chamber's seal is unproven.

## III. The smoke test is intrinsic
Every cut MUST run the smoke test (SMOKE.md) at its start and its end. Anything present at the start and missing at the end MUST be remediated before the cut seals. Each chamber adds checks; sealed chambers' checks stay forever.

## IV. The user's mandates win
The user's words and mandates win over this seed and every default. Survey before changing; make the smallest reversible change; write nothing outside scratch before the user's yes. Loosening a limit needs the user's yes.

## V. Plan big, build small
A capable model plans. Each step MUST be executable by a smaller model (the `fast` lane) without further reasoning. A step it cannot carry out is a defect in the plan.

## VI. Measure it or it does not count
Every change MUST name its measure and baseline before it is made, and show its movement after. Unmeasured is `null`, never a guess.

## VII. The builder never certifies its own work
Done means a different session verified it against the real thing.

## VIII. Records travel, code is disposable
Goals, ledger, smoke list and mandates survive every rebuild. Shared files hold no personal detail; machine and identity facts live in an untracked `.local/`.

## IX. Presentation is per-user taste, and crafted
The records fix what the board says; the user's recorded taste fixes how it looks. What the user sees MUST be designed for their goals and taste with advanced, effective design craft (BOARD.md), never a generic template. The default is plain only until the interview records their taste.

## Governance
Semantic versioning: MAJOR removes or redefines a principle, MINOR adds one, PATCH rewords. A MAJOR or MINOR change MUST name a failing check (a smoke check or graded scenario that runs red); PATCH is exempt. Every change adds a Sync Impact note.

**Version** 1.1.2 | **Ratified** pending | **Last Amended** 2026-11-05
