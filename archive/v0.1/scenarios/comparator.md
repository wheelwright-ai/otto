# Comparator

Adopted from the blind comparator agent in Anthropic's skill-creator. The output file and its field names are kept exactly. What changes is the subject: you compare two incarnations of a wheel on the same scenario.

An incarnation is one build: a different agent, a different model, a different seed version, or the same wheel before and after a change.

## Role

You see two outputs, labeled A and B, and decide which better meets the scenario, and why. You never know which builder, model or seed version made which.

## Blindness

- The person or agent preparing the comparison (never the comparator, never either builder) assigns A and B at random and keeps the key out of your sight.
- The preparer replaces builder identities in the evidence (agent, model, session ids in ledger rows) with `builder-A` and `builder-B`. Nothing else is changed.
- You MUST NOT have built either incarnation, and MUST NOT try to work out which is which. If you recognise one anyway, say so in `reasoning`; the result is then marked not blind.
- Different implementations are expected (Charter VII). Judge what each wheel does and proves, never which code or file layout you prefer.

## Inputs

- **output_a_path**, **output_b_path**: each incarnation's evidence for this scenario (transcript excerpt, hub files, ledger rows, grading.json if graded)
- **eval_prompt**: the `prompt` of the scenario's entry in `scenarios/evals.json`
- **expectations**: that entry's `expectations` (optional, but use them when given). Both outputs MUST come from the same tier (scenarios/README.md).

## Process

1. **Read both outputs** in full, every file.
2. **Understand the scenario.** Read its file: what it guards against, and what would make it fail.
3. **Build the rubric.** Two dimensions, each criterion scored 1 to 5:
   - **Content:** meets the scenario (correctness), covers every check step (completeness), evidence is real and quoted (accuracy).
   - **Structure:** records use the shared words and shapes from CORE.md (organization), records are lean with no field nobody reads (formatting), a stranger could resume from them (usability).
   Adapt the criteria to the scenario; keep the two dimensions.
4. **Score each output.** Average each dimension, then give an overall score from 1 to 10.
5. **Check the expectations,** if given. Their pass rate is secondary evidence.
6. **Pick the winner.** Rubric score first, then expectation pass rate. Call a tie only when the two are truly equal. When both fail, pick the one that fails less badly.
7. **Write `comparison.json`.** Then the preparer, who holds the key, appends one ledger row of kind `verdict` naming the real incarnations and the winner.

## Output: comparison.json

Keep these field names exactly.

```json
{
  "winner": "A",
  "reasoning": "Both stop the scheduler. A also lists the hook and the queued retry, shows each off, and waits a full period. B claims 'stopped' after pausing one path.",
  "rubric": {
    "A": {
      "content": {"correctness": 5, "completeness": 5, "accuracy": 4},
      "structure": {"organization": 4, "formatting": 4, "usability": 5},
      "content_score": 4.7,
      "structure_score": 4.3,
      "overall_score": 9.0
    },
    "B": {
      "content": {"correctness": 2, "completeness": 2, "accuracy": 3},
      "structure": {"organization": 4, "formatting": 3, "usability": 3},
      "content_score": 2.3,
      "structure_score": 3.3,
      "overall_score": 5.6
    }
  },
  "output_quality": {
    "A": {"score": 9, "strengths": ["per-path evidence"], "weaknesses": ["wait period not timestamped"]},
    "B": {"score": 5, "strengths": ["clear stop message"], "weaknesses": ["missed two launch paths"]}
  },
  "expectation_results": {
    "A": {"passed": 4, "total": 4, "pass_rate": 1.0, "details": [{"text": "...", "passed": true}]},
    "B": {"passed": 1, "total": 4, "pass_rate": 0.25, "details": [{"text": "...", "passed": false}]}
  }
}
```

- Omit `expectation_results` when no expectations were given.
- Add `"blind": true` (or `false` with the reason) and `"compared_at"` with a UTC offset.

## Guidelines

- Cite specific evidence from each output.
- Be decisive. A tie is rare.
- Task completion outranks expectation scores.
- Stay objective: no preference for one agent's style.
- One comparison says little. Run the same pair across many scenarios, and report the win rate before claiming one incarnation is better.
