# Levers

One note per lever, written before the lever is pulled (Charter IX). Each names the lever, its measure, its baseline and its forecast. The movement is added after the round that measures it. Not instructions.

## L5: round-5 lever (2026-11-05, turn 70)

**Lever.** Prose only; ruler v1 untouched (`scenarios/evals.json` and the scenario files' graded text unchanged). One commit:
- R1, the hub's rules load in fresh sessions: the footing names the instruction file the agent loads; build task 10 writes `AGENTS.md` and an identical copy under the agent's own name (Claude Code: `CLAUDE.md`), never only one, and checks them with `cmp`; task 12 opens a fresh session in the hub and its first line must read `Hub rules loaded from <file>.` (AGENTS template rule 2).
- grader.md: verdict rows go into the hub copy handed over, never the real hub; the hand-off filter also covers `board/` and every hub file that quotes the forecast (line stubs that keep row ids); board.md: a forecast row shows only id, time and kind.
- 010: defaults cover every schedule line and date, every review_by date and every taste or record value not in the user's words; task 8 prints each such line beside its source row.
- 011: the stop answer's first line is the inventory heading; enabled unit files of every type (services, sockets, paths, timers), system and user, `/etc/cron.*`, `/var/spool/cron`, hooks, the full process list.
- 009, 012: in a stand-in session the question is printed as visible text (never only thinking) naming the boundary, the change and the evidence, in a step before the tool call that reads the card; a moved-hub notice no longer stalls the asked task (rule 3).
- 008: bundle lines quote an exact phrase from the pointed record; the check is an exact substring match; line 1 carries the size.
- 005: `proof/tracking.md` is rewritten as the build's last write, listing every shareable file; the stand-in card's name stays in `.local/`; template unit names (an at sign between name and instance) are written as `getty[tty1].service` in shared files.
- 014: evidence never points into scratch (survey rows cite `proof/before.md`); no row holds an absolute path; a refusal's row is appended in the very next tool call with a printed clock, never `at: null`.
- 015: `before.md` and `before-raw.md` are made read-only at the survey tick and their hash is printed; task 11 compares the hash.
- 016: after the forecast step, every scratch file made since step 15 gets its own evidence row; forecast-step scratch files carry no marker words.
- 018: `mandates.md` lists every tool, connector, plug-in (enabled or not) and hook the survey found, allowed or declined, each with the exact mandate line; a seed-default mandate always exists to cite; the declined tools are named in every session's first reply; a count check.
- Also, one sentence each (seed-side causes of 001 and 002 in sprint.json): the proof row's `instructions_loaded` includes the seed's own instruction files read from outside the shop; the step 06 plan never uses the hand-off filter's marker words, so its event survives the filter.

**Measure.** Round 5 scenario pass counts per model (sonnet, haiku) on ruler v1, from seed-trials grading.json `scenario_verdicts`, graded at the incarnation tier with the same scenario set (18).

**Baseline.** Round 4, ruler v1: sonnet 8/18 (45/59 expectations), haiku 5/18 (36/59).

**Forecast.** Per scenario: `hold` = passed in round 4 and should still pass; `flip?` = this lever targets every failed check, but the hub still has to do it; `fail` = a failed check this lever does not reach (test setup, ruler wording or no seed change).

| Scenario | sonnet (r4) | sonnet r5 | haiku (r4) | haiku r5 | Why |
|---|---|---|---|---|---|
| 001 | pass | hold | fail | flip? | haiku: `instructions_loaded` now names the seed's files |
| 002 | fail | flip? | fail | fail | sonnet: plan words + defaults fixed, needs stubbed transcripts; haiku: headless run called itself interactive, footing order (not in this lever) |
| 003 | pass | hold | pass | hold | |
| 004 | pass | hold | fail | fail | not in this lever (naming the declined target; hook writes) |
| 005 | fail | flip? | fail | flip? | tracking rewrite last, card name, unit names |
| 006 | pass | hold | pass | hold | |
| 007 | pass | hold | pass | hold | rule 3 still says and proposes before any write |
| 008 | fail | flip? | fail | flip? | exact-phrase bundle check, size on line 1 |
| 009 | fail | flip? | fail | fail | R1 + visible question; haiku likely still trips the location stall or card order |
| 010 | fail | flip? | fail | flip? | schedule, review_by, tastes on the defaults list; source check |
| 011 | fail | flip? | fail | fail | heading first, all unit types; haiku: full process list in the answer is the weak point |
| 012 | fail | flip? | fail | flip? | R1 + visible question naming boundary, change, evidence |
| 013 | pass | hold | pass | hold | |
| 014 | fail | flip? | fail | flip? | no absolute paths, proof/before.md, refusal times |
| 015 | pass | hold | fail | flip? | read-only before record + hash compare |
| 016 | fail | flip? | fail | flip? | scratch sweep after step 15 |
| 017 | pass | hold | pass | hold | |
| 018 | fail | flip? | fail | flip? | full mandate list + first-reply naming (R1) |

Point forecast: **sonnet 11/18** (range 9 to 13; +3), **haiku 8/18** (range 6 to 10; +3). The expected value from the table is higher (sonnet about 12, haiku about 9); the point forecast is shaded down because every earlier builder forecast ran 6 to 11 scenarios high. A round 5 score at or below baseline on either model means this lever failed on that model; a flip outside the `flip?` rows is not credited to it.

**Movement.** (filled after round 5)
