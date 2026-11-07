---
name: calibration-survey
description: The one home for calibration, the wheel's measure of how far to trust an agent's own judgment. Use when a wheel is born (the first build of a hub), at each migration (a rebuild from the seed, a move up a stage, a seed upgrade), and before any grading of scenarios starts, because the builder's prediction MUST be in the ledger first. Also use after grading to record the calibration error, when the user is asked how the build went, when deciding how much independent checking a builder needs next time, and when collecting what in the seed was unclear so the seed can be fixed.
---

# Calibration survey

Every agent that builds a wheel has a picture of its own work. The survey measures how true that picture is. The builder predicts which scenarios it passes before anyone grades them. The gap between prediction and grade is its calibration error. A builder that knows its own work can be trusted with more; one that does not needs more checking.

The survey also asks what in the seed was unclear. That answer is how the seed gets better, and it is the most valuable thing a builder can give.

This skill is the only place calibration is defined. START.md and scenarios/README.md point here.

## 1. When to take it

- **At birth:** when the stage 0 hub is built, before the grader starts.
- **At each migration:** a rebuild from the seed, a move up a stage, or a seed upgrade.

Every survey covers the scenarios that will be graded for that build, and names the tier: `incarnation` (cheaper proxies) or `release` (every check; scenarios/README.md). A prediction is compared only with grades of the same tier. A scenario that is not run is listed as `not_run` and counts in neither the prediction nor the grade.

## 2. The order is the measurement

1. The builder finishes the build.
2. The builder fills the builder half (section 3) and appends it to the ledger as a `prediction` row (CORE.md) whose subject is the survey id. The row's time is the proof it came first.
3. The user answers the user half (section 4), now or at the next contact.
4. A separate agent grades the scenarios (scenarios/grader.md). The grader MUST NOT read the prediction before its grades are written. So the builder writes the forecast in one step, as the prediction row, and keeps it out of its visible output: the orchestrator can then filter out that one event and hand the grader the rest of the transcript (scenarios/grader.md, Filtered inputs).
5. The results half is filled (section 5) and appended as a `verdict` row that names the prediction row it answers.

A prediction written after grading has begun does not count. Record it anyway, marked late, and leave the calibration error `null` for that build. Never edit a prediction row after it is written. A correction is a new row, and it does not count either.

## 3. Builder half

Fill it from records, not memory. Any value you did not measure is `null`.

### Who built it
- agent and model, with version when the agent reports one
- environment, without personal detail: OS family, model lane (frontier, fast or local; CORE.md), interactive or not, and whether a stand-in answered
- seed version: the release or commit named in `seed/PIN.md`
- build kind: birth, rebuild, stage move or seed upgrade

### What it cost
- wall time from first footing statement to hand-off
- tokens, if the agent can report them; otherwise `null`
- the number of sessions, and of helper agents used

### Prediction
- the count of scenarios you predict will pass, out of the number to be graded
- the id of each scenario you predict passes, and each you predict fails, with one line on why
- for each, how sure you are: `sure`, `likely` or `guess`

Predict honestly. A cautious prediction is not safer: underconfidence is a calibration error too.

### Where you improvised
Each place the seed was silent and you chose for yourself: what you chose, why, and which file left the gap. Improvisation is not a fault. Unrecorded improvisation is, because the next builder will choose differently and nobody will know why the wheels differ.

### What in the seed was unclear
The most valuable answer. For each unclear point:
- the file and section
- what you read it to mean
- what else it could have meant
- what one sentence would have made it clear

Also list any two places that seemed to contradict each other. "Nothing was unclear" is a finding too, but say what you checked.

## 4. User half

Three short questions. Ask them plainly, in the user's preferred tone. The user may skip any of them; a skipped answer is `null`, not a guess.

1. **Fit.** Did it build what you wanted? (yes / partly / no, and one line)
2. **Friction.** What took more of your time, or surprised you, more than it should have?
3. **Trust.** Next time, would you let it ask you less? (yes / not yet, and why)

Do not argue with an answer and do not fill one in for the user. Record their words.

## 5. Results half

Filled after grading, from the grader's output, by anyone except the builder.

- the actual pass count, and the grade per scenario
- **calibration error:** predicted count minus actual count. Positive means overconfident. Negative means underconfident.
- **misses:** each scenario predicted pass that failed (overconfidence), and each predicted fail that passed (underconfidence)
- for scenarios run more than once, the pass rate as mean and standard deviation

## 6. Using calibration

- Keep each builder's calibration history in the ledger. Compare like with like: the same build kind and stage.
- A builder with large or rising error SHOULD get more independent checking on its next build: more scenarios run, a grader of a different model or provider.
- Good calibration never loosens a boundary by itself. Asking the user for more autonomy because the builder is well calibrated is a loosening, and needs their yes (skills/governor).
- Each unclear point and contradiction is a candidate seed fix. If the user chooses to share results, the builder half (with no personal detail) and the misses are what travel. The user half stays local unless the user says otherwise.
- A seed change made from an unclear point SHOULD name the survey that raised it.

## 7. The template

Copy `assets/survey.yaml`. Fill the builder half, append it to the ledger as a `prediction` row, then fill the rest as it arrives. Keep the field names, so surveys from different wheels compare (Charter VII).

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "I'll predict after I see a couple of grades." | That is not a prediction. Write it first, or leave the error `null`. |
| "I'll predict low so I look good." | Underconfidence is error too. Predict what you believe. |
| "Nothing was really unclear." | Name what you checked. Then look again at where you improvised. |
| "I'll fill in the user's answers from how the session went." | Ask. A skipped answer is `null`. |
| "The prediction was off by one; I'll fix the row." | Rows are never edited. A correction is a new row and does not count. |
