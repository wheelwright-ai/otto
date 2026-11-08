# WORK

How a work item moves, and how the ledger records it. The wheel keeps its own `WORK.md` (the items) and `ledger.jsonl` (the rows).

## Plan, execute, verify
Every item passes through three hands. The verifier is always a different session from the planner and the executor (Charter VII).
1. **Plan** (a `frontier`-lane session whenever one is available). Writes the item: its goal, its measure with a baseline, its lane, its verifier, its steps and its check. Each step is a literal action a `fast` model can do without choosing anything: a file and its exact content, a command and its expected output. A step that needs judgment is split or rewritten before execution (Charter V). With no `frontier` session available, a `fast`-lane builder may plan its own items: it records `planner_lane: fast` on the item and its `plan` row, and the board shows it.
2. **Execute** (the named lane). Does the steps in order and nothing else, then records what each step printed. It never writes `verified`.
3. **Verify** (the named verifier). Runs the item's check against the real thing and appends a `verdict` row: `pass` or `fail`, with the output quoted. Only a `pass` verdict moves the item to `verified`.

**A check the verifier cannot run itself** (its sandbox refuses the command, or the output is too large to read) fails on access, not on substance. The planner prevents that: before the verifier starts, it exports what the check needs to files the verifier can read (for example `.local/<item>/`: a file's content at a commit, a diff summary, the exit codes of commands it ran), and the check names those files. The verifier still judges the evidence itself; when it doubts an exported file, it says so and the item stays unverified.

**A verifier whose ledger append is blocked** (a guard, a read-only sandbox) prints its verdict row as visible output: the full JSON row, without `id` and `at`. The executor appends that row verbatim, adding only `id`, `at` (its own clock reading, as for any row it appends) and `appended_by` naming itself (`{"role": "executor", "session": "s-1"}`). The verdict's `actor` stays the verifier; the executor never edits the text, result or evidence.

## Item shape
```yaml
- id: W-001                 # never reused
  goal: G-001               # an active goal (smoke S-0-01)
  measure: {metric: <what moves>, baseline: <value or null>, target: <value>, source: <where read>}
  lane: fast                # frontier | fast | local
  planner_lane: frontier    # frontier | fast (a fast builder that planned its own item)
  verifier: "a session other than the planner's and the executor's"
  steps:
    - "<literal action and its expected output>"
  check: "<command or observation, and the output that means pass>"
  state: planned            # planned -> executed -> verified | failed; or dropped (with a reason row)
  rows: []                  # ledger row ids for plan, execute, verdict
```
Open means `planned`, `executed` or `failed`. A `failed` item is replanned or dropped with a reason.

## Ledger
`ledger.jsonl`: one JSON object per line, appended, never edited. A correction is a new row with `supersedes`.

```json
{"id": "r-000007", "at": "2026-11-05T14:12:03-08:00", "cut": 1, "kind": "verdict", "subject": "W-001", "actor": {"role": "verifier", "session": "s-3", "model": "<model id>"}, "text": "check output matched", "evidence": ["<quoted output or tracked path>"]}
```
- Kinds: `cut` (with `phase`: `open` | `seal`), `goal`, `smoke`, `plan`, `execute`, `verdict`, `remediation`, `decision` (a default, a taste, the yes), `ruling` (a mandate or a budget boundary in the user's words), `foreign` (something another tool on the machine owns: a file it wrote into the wheel, with `pattern`, `tool`, `first_seen` row id, smoke S-0-07; or a global install the first cut's survey found, with `scope` (`user` or `machine`), `what` (settings, hook, tool server, plugin, skill) and `name`, never an absolute path; set aside, never changed). Interview rows also carry `topic`: `goal`, `direction`, `budget`, `progress`, `taste` or `foreign` (GOALS.md); a wave's board review carries `topic: board_review` (WAVES.md).
- `at` MUST be copied from a clock reading printed in the same tool call that appends the row. Never type, round or space out a time.
- Ids run `r-000001`, `r-000002`, ... with no gap (smoke S-0-02).
- `evidence` points only at tracked files, by relative path, or at row ids; never into `.local/` or scratch. No row holds a name, an email or an absolute path.
- `usage` (optional) on a `plan`, `execute` or `verdict` row: the tokens the session spent on that step, as `{"model", "input", "output", "cache_read", "cache_create"}` with integer counts copied from the agent's own report, never estimated, or `null` with `usage_reason`. Claude Code reports them with `claude -p --output-format json`: `usage.input_tokens`, `usage.output_tokens`, `usage.cache_read_input_tokens`, `usage.cache_creation_input_tokens`.
- A value not measured is `null`.
