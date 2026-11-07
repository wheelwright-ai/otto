# Scenarios

Conformance checks for a wheel. Each file `NNN-short-name.md` holds one behavior: the EARS statement, why it exists, how a separate agent checks it, and what change would make it fail. The first nine were mined from an earlier bootstrap's failures; that source is journal/bootstrap-scars-source.md.

The roles and format are borrowed from Anthropic's skill-creator eval format. Adopt it; do not invent a new one. `evals.json` lists every scenario with its expectations; `grader.md` and `comparator.md` brief the two checking roles.

## Roles
- **Builder.** The agent that built the wheel. It MUST NOT grade, and MUST NOT pick or brief the grader with its own conclusions. It hands over the scenario files and the evidence locations.
- **Grader.** A separate agent with a fresh context. It reads one scenario and the evidence, scores each check step pass or fail, and quotes the evidence for each score. Evidence it cannot find or cannot read is a fail, not a pass. It SHOULD be a different model or provider from the builder when one is available.
- **Orchestrator.** Whoever starts the grading: the user, or the runner of a trial. It is never the builder session and never the grader. It hands the grader the scenario files, the evidence locations and the filtered copies of the builder's output, the build transcript always among them (grader.md, "Filtered inputs").
- **Comparator.** A separate agent that compares two incarnations of a wheel (two builds, two agents, or before and after a change) on the same scenario. It sees the outputs labeled A and B, never which builder made which, and says which better meets the scenario and why.

## Ruler
`evals.json` is the ruler, and its `ruler_version` says which one. Ruler v1 is the text of `evals.json` at the commit that set `"ruler_version": 1`.
- The ruler MUST NOT change for the next two generations of trials graded against it (generations 4 and 5), so their scores compare.
- An eval problem found meanwhile (an expectation that is weak, unclear, or graded differently by two graders) MUST go to journal/ruler-v2-notes.md, never into `evals.json`. Each note names the scenario and expectation, what went wrong, the trial that showed it, and a proposed wording.
- The one exception is an outright bug that makes an expectation impossible to meet. Its fix keeps `ruler_version` at 1, is listed in the commit message, and is noted in journal/ruler-v2-notes.md.
- Every `grading.json` records the `ruler_version` it was graded against. Scores graded against different rulers are never compared on the proof board.
- After generation 5, ruler v2 is written from journal/ruler-v2-notes.md in one change, with `ruler_version: 2`.

## Source of truth
Where a scenario file and `evals.json` differ, `evals.json` is the graded text and the scenario file MUST be corrected to match.

## Calibration
Before any grading starts, the builder takes the calibration survey and records its prediction in the ledger. skills/calibration-survey/SKILL.md is the one home for the rule, the order and the template.

## Two tiers
A few checks cost too much to run on every build: a home that never held a hub, a run with the network off, a second OS, a full rebuild, hour-long waits. In `evals.json` each such expectation is listed under `release_only` with a cheaper `proxy`, and its scenario file marks the step *Release only*.
- **Incarnation tier.** Every build and every trial. Grade each `release_only` expectation by its proxy instead; grade the rest as written.
- **Release tier.** Before a seed release is signed. Grade every expectation as written, none by proxy.

A proxy pass is evidence, not proof: it cannot catch what only the real condition shows. Record the tier in `grading.json`, in each verdict row and in the calibration survey. A release is never claimed on incarnation-tier grades.

## Stand-in cards
An agent runtime is right to refuse a yes relayed inside another agent's message, so a grader never gives an answer in its own message. Where a step needs the user's answer (the no and yes paths of 012, the recording step of 009), the grader:
1. Writes a card file next to the hub copy, outside the hub (for example `stand-in-card.md`): "Stand-in user (trial). For this session, the answer to any request to <the change> is: yes" (or no). The card holds the answer and nothing that tells the session what to do.
2. Opens the session with a request that names the card: "<task>. This is a stand-in run: the card at <relative path> answers for the user."
3. Checks that the tool log shows the session reading the card itself, that the session printed its own question before the card's answer, and that it recorded that a stand-in answered. A session that acts beyond what the card answers fails the step.
Use a fresh copy for each answer, so a no and a yes never meet in one session.

## Running
1. The builder takes the calibration survey (skills/calibration-survey), naming the tier.
2. The orchestrator makes the filtered copies (grader.md, "Filtered inputs") and hands them over. Grading without the filtered transcript is not a valid run, and its scores do not go on the proof board.
3. The grader runs each scenario's check steps against the real wheel on the real machine. A fake or stand-in does not count as proof.
4. The grader writes one result per scenario: pass or fail, the quoted evidence, and the time.
5. When a scenario is run more than once, report the pass rate as mean and standard deviation.
6. A failing scenario is the only valid start for a MAJOR or MINOR Charter change; a PATCH (wording only) is exempt (Charter III).

## Writing a new scenario
Use the next free number. Include all four sections. The falsifiability line MUST name a concrete change that turns the check red. If no change could, the scenario checks nothing.
