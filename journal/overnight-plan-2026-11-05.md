# Overnight plan, 2026-11-05 (operator asleep)

Mandate (operator, 12:19 AM PST): "build this out completely and test it before applying it to our live projects."
Hard line: NOTHING is applied to any live project tonight. All trials run in the separate seed-trials repo.

## Steps (each lands with a journal line; the main session drives, helpers write)
1. Wave 3, two builders in parallel:
   - A: skills/tread, skills/sharing-flavors, list every skill in llms.txt.
   - B: OUTLINE "wave 3" open items (CORE prediction kind + group term, governor at stage 0 + START pointer + engagement-guide stage fix, evals.json costly scenarios marked release-only with cheaper proxies, DESIGN build task 6 proof wording).
2. Independent review of the whole seed by an agent that wrote none of it: contradictions, gaps, anything a stranger's agent could not follow. Fix pass on the findings.
3. Generation 1 incarnations, built from the seed ALONE, in seed-trials/gen1-<model>/shop/ with a fictional stand-in user (no real personal detail):
   - two builders on different models (variation is by design).
   - each takes the calibration survey and records its prediction BEFORE grading.
4. Grading: a grader on a different model from the builder follows scenarios/grader.md and writes grading.json per incarnation. A blind comparator compares the two.
5. Fix the seed from failures and the survey's "unclear" answers. If there is time, run generation 2 and compare.
6. Morning report: the proof board (incarnation, model, environment, scenarios passed X of N, prediction vs actual, rolling y/n), what changed in the seed, what needs the operator.

## Known limits, said up front
- Scenarios that need a never-used machine or a network-off run are release-only; tonight uses the cheaper proxies.
- The stand-in user is a fiction; the first real interview is the operator's.

## Follow-ups queued for step 2 (from wave 3A, 12:27 AM)
- CORE: add flavor and item glossary entries
- hub/DESIGN layout: add the tread/ folder
- Release signing: which keys to trust (needs a concrete answer before the first fleet release; operator decision)
- Who decides adoption before stage 2: the hub agent runs the loop, the user decides
