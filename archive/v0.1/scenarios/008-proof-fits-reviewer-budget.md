# 008: Proof fits the checker's input budget

## Statement
WHEN proof is handed to a checker, THE HUB SHALL fit it within the checker's input budget, with pointers to the full evidence, and SHALL NOT truncate it silently.

## Why
An independent review failed because the evidence was cut from about 320 KB to 131 KB on the way in; the checker judged a fragment and the work was never certified. Proof the checker cannot read in full is not proof.

## How a separate agent checks it
1. Find the evidence bundle handed to the grader (`proof/bundle-<date>.md`, hub/DESIGN.md build task 14). Measure its size.
2. Compare with the grader's stated input limit: the `grader input limit` in `steering/records.md`, or 100 KB when it is unset. The bundle MUST be at most half of it, leaving room for the scenario and the reply.
3. Each pointer in the bundle MUST resolve to a real file or record, found by its exact id (not a pattern), and the record MUST show what the bundle line says it shows.
4. Confirm the grader's input was not cut: the last line of the bundle appears in what the grader received.
Pass when the bundle fits, every pointer resolves, and nothing was truncated.

## Falsifiability
Fails if a bundle larger than the grader's limit is sent, if a pointer leads nowhere, or if the grader's input ends before the bundle does.
