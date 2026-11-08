# WORK

How a work item moves, how it is grouped and proven, how work is saved, and how the ledger records it. The wheel keeps its own `WORK.md` (the items) and `ledger.jsonl` (the rows).

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

## Lugs and initiatives (from wave 1)
From wave 1 every item is a **lug**, and lugs are grouped into **initiatives**. A lug keeps the item shape above and adds:
```yaml
  title: "<what it delivers, in plain words>"
  initiative: I-001         # exactly one; the lug takes the initiative's goal
  value: 3                  # 1-5: what it is worth to the goal
  effort: 2                 # 1-5
  kind: autopilot           # autopilot (has a check another session runs) | owner (only the user can do it)
  rank: 4                   # unique among open lugs: 1..N, no gaps
```
- **Status:** `proposed` -> `planned` -> `executed` -> `verified`, or `failed`, `blocked` or `dropped`; open means any but `verified` and `dropped`. The plan, execute and verdict rows record those moves; every other change (added, ranked, blocked, dropped, edited, moved to another initiative) is a ledger row of kind `lug` naming who made it and why. Nothing is overwritten: a lug's state is the replay of its rows, and WORK.md is regenerated from them, never edited by hand.
- **Rank:** a new lug is placed by value against effort (for example value x 2 - effort), or by judgment, and its row records the position and the reason. Ranks the user pinned stand. No lug ranks above one it depends on. When a lug closes, the ranks below it move up.
- **Kind:** an autopilot lug names its check, and a different session closes it (above). An owner lug is the user's: ask for it in one line (Proof) and record the answer.

An initiative serves one agreed goal (GOALS.md) and holds the lugs that deliver it:
```yaml
- id: I-001
  goal: G-001
  title: "<plain words>"
  outcome: "<what is true when it is done>"
  why_now: "<why this before other work>"
  scope: {in: "<the lugged work>", out: "<what it will not do>"}
  done_when: "<a number or an observable result someone else can check>"
  signoff: null             # or the row id quoting the user's yes
```
- **Written, not filled in.** Every section says something: no empty or placeholder text (tbd, n/a, `...`); outcome and done_when are at least eight words; done_when names a number or an observable result, never an unpinned "better" or "improved". The wheel builds a lint that refuses an initiative breaking any of these; then a fresh reader checks the sense (Proof). Headings alone can be filled with nonsense.
- **Progress is computed, never typed:** verified lugs over lugs not dropped (a dropped lug never counts as done). Status follows: `proposed` (nothing started), `active`, `done` (every counted lug verified), `dropped` (every lug dropped). Closing an initiative while any of its lugs is open is refused.
- **The user signs off** each initiative (a `decision` row quoting their yes) before any autopilot work is spent on its lugs. Changing its goal, outcome, scope or done_when puts it back to awaiting sign-off.
- Initiative changes are ledger rows of kind `initiative`, like lugs.

## Proof
- The builder never certifies its own work (Charter VII): a session that did not build it runs the check.
- Anything written for the user to read or decide on (an initiative, a summary, a plan, a review page) gets a fresh-reader pass before it reaches them: a session that did not write it reads it cold and checks that every claim is backed by its done_when or by evidence, the scope covers only lugged work, nothing is ranked above what it depends on, and there is no jargon or id the user would not know. Fix what it finds, with reasons, and have it read again.
- Ask the user in one line per item: what you need, the choices and your recommendation. Never pages; detail on request.

## Saving work (from wave 1)
For the wheel and every project it looks after, when it is a git repository:
- **One worktree per session.** Every session starts from the project's main branch in a fresh worktree on its own branch (`wheel/<date>-<session>`), never in the main checkout, so who is doing what, and where, is always visible. The main checkout stays clean.
- **Save at the end of every turn.** Commit only the files that turn changed, by name (never everything), after a secrets scan of them. The message says what was being worked on: the user's ask in one line, the files, the session id. Skip, and log why, when the scan finds something, a merge or rebase is in progress, or a file looks generated. A turn save never pushes; pushing follows the user's rule.
- **Ignore what must not travel.** Each project's `.gitignore` covers secrets, dependencies, caches, build output and `.local/`, so a save can never pick them up.
- **Finish the branch.** When the work is verified, merge it into main and remove the worktree. A project that publishes live when main changes waits on its branch until the user accepts the work.
- **Tidy at wake-up.** Look at every worktree and branch: merged ones are removed; uncommitted work in a worktree is saved on its branch first (after the scan); a finished branch that merges cleanly with its tests passing is merged only if the user has said so; anything else gets one line asking the user. Each action is a ledger row; the first tidy is a dry run shown to the user.

## Ledger
`ledger.jsonl`: one JSON object per line, appended, never edited. A correction is a new row with `supersedes`.

```json
{"id": "r-000007", "at": "2026-11-05T14:12:03-08:00", "cut": 1, "kind": "verdict", "subject": "W-001", "actor": {"role": "verifier", "session": "s-3", "model": "<model id>"}, "text": "check output matched", "evidence": ["<quoted output or tracked path>"]}
```
- Kinds: `cut` (with `phase`: `open` | `seal`), `goal`, `smoke`, `plan`, `execute`, `verdict`, `remediation`, `decision` (a default, a taste, the yes), `ruling` (a mandate or a budget boundary in the user's words), `lug` and `initiative` (from wave 1: every change not recorded by a plan, execute or verdict row, with who and why), `foreign` (something another tool on the machine owns: a file it wrote into the wheel, with `pattern`, `tool`, `first_seen` row id, smoke S-0-07; or a global install the first cut's survey found, with `scope` (`user` or `machine`), `what` (settings, hook, tool server, plugin, skill) and `name`, never an absolute path; set aside, never changed). Interview rows also carry `topic`: `goal`, `direction`, `budget`, `progress`, `taste` or `foreign` (GOALS.md); a wave's board review carries `topic: board_review` (WAVES.md).
- `at` MUST be copied from a clock reading printed in the same tool call that appends the row. Never type, round or space out a time.
- Ids run `r-000001`, `r-000002`, ... with no gap (smoke S-0-02).
- `evidence` points only at tracked files, by relative path, or at row ids; never into `.local/` or scratch. No row holds a name, an email or an absolute path.
- `usage` (optional) on a `plan`, `execute` or `verdict` row: the tokens the session spent on that step, as `{"model", "input", "output", "cache_read", "cache_create"}` with integer counts copied from the agent's own report, never estimated, or `null` with `usage_reason`. Claude Code reports them with `claude -p --output-format json`: `usage.input_tokens`, `usage.output_tokens`, `usage.cache_read_input_tokens`, `usage.cache_creation_input_tokens`.
- A value not measured is `null`.
