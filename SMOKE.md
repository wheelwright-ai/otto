# SMOKE

The living smoke test: what MUST be there at the start of every cut, and still there at its end. The wheel keeps its own `SMOKE.md`, first copied from the checks below; every cut may add to it.

## Expectation shape
```yaml
id: S-0-01            # S-<wave>-<number>; never reused
wave: 0
expects: what must exist, in one sentence
check: |              # mechanical: commands or observations a fast model runs as written
  the steps, and the output that means pass
added_in_cut: 0       # 0 = shipped with the seed; otherwise the wheel's cut number
retired: null         # or {row: r-000123, reason: "..."}; only for a check of the open wave
```

## Rules
- Every cut MUST run every live check at its start (START step 02) and its end (step 06). Each run appends one ledger row: `{"kind": "smoke", "check": "S-0-01", "phase": "start" | "end", "result": "pass" | "fail" | "not_run", "evidence": "<the output that decided it>"}`.
- `not_run` MUST carry a reason. A check skipped without one counts as `fail`.
- A check that passed at start and fails at end MUST be remediated (START step 07) before the cut seals: fix it, re-run it, append a new `end` row and a `remediation` row naming both.
- A check that fails at start becomes a work item in that cut's plan.
- A check MAY be removed only with a ledger `decision` row giving the reason, and only while its wave is open. Sealed waves' checks stay forever.
- Each wave adds its own checks before it can seal. Each cut SHOULD propose a check for anything it found missing (START step 09).
- A check MUST say what output means pass, and name a change that would turn it red. A check no change could fail checks nothing.

## Checks: wave 0

### S-0-01 Goals drive the work
- expects: `GOALS.md` exists with at least one active goal that has a measure, and every open work item names an active goal.
- check: (1) `GOALS.md` exists. (2) It lists at least one goal with `status: active` and a `measure` with `metric`, `baseline` (a value or `null`) and `target`. (3) For every item in `WORK.md` whose `state` is `planned`, `executed` or `failed`, its `goal` is the id of an active goal. Pass: all three hold. Red if: an item names a dropped goal, or none.
- added_in_cut: 0

### S-0-02 The ledger is sound
- expects: `ledger.jsonl` parses, its ids run in order, and every `at` is a real clock time with offset, never backwards and never in the future.
- check: (1) Every line parses as one JSON object. (2) The ids are `r-000001`, `r-000002`, ... with no gap or repeat. (3) Every `at` matches `YYYY-MM-DDTHH:MM:SS±HH:MM`. (4) No `at` is earlier than the row before it. (5) No `at` is later than the clock read at the check. Pass: all five hold. Red if: a typed or rounded time runs backwards, or a row is edited out.
- added_in_cut: 0

### S-0-03 The last cut was smoked both ways
- expects: the last sealed cut has one `start` and one `end` smoke row for every check that was live at its start.
- check: (1) Find the last `cut` row with `phase: seal`, and the same cut's `phase: open` row. (2) List the checks live at that open (from `SMOKE.md`, using `added_in_cut` and `retired`). (3) For each, find one `smoke` row with `phase: start` and one with `phase: end` in that cut. Pass: every check has both. No cut sealed yet: `not_run`, reason "no sealed cut". Red if: a cut seals without its end smoke.
- added_in_cut: 0

### S-0-04 The board is true to the ledger
- expects: `BOARD.md` names the ledger's last row, or says it is stale, and regenerating it gives the same board apart from its stamp.
- check: (1) No `BOARD.md` yet: `not_run`, reason "no board yet", allowed only before the first step 08 of cut 1 (the ledger's only `cut` row is cut 1's `phase: open`); a missing board at any later point is fail. Otherwise read the row id in the board's first line. (2) If it is the ledger's last row, go on; if it is an earlier row, print `STALE board: <board row> < <last row>` and go on; if it is no row in the ledger, fail. (3) Regenerate the board (BOARD.md rules) from the ledger up to that row, into scratch. (4) Compare it with `BOARD.md`, ignoring line 1. Pass: no difference. Red if: a number on the board was typed by hand.
- added_in_cut: 0

### S-0-05 No personal detail travels
- expects: no shared file holds personal detail, and `.local/` is ignored.
- check: (1) `.gitignore` has the line `.local/`. (2) In a git wheel, `git check-ignore -q .local/probe` exits 0. (3) Search every tracked file for: the user's name and account name (read from `.local/`), the machine's hostname, any email address, and any absolute path: a path that starts at the filesystem root and names a home or users folder, or a path that starts with a drive letter and a colon. Describe these patterns in words, never as a literal path, so this text does not trip its own check. Pass: (1) and (2) hold and (3) finds nothing. Red if: a ledger row names the user.
- added_in_cut: 0

### S-0-06 A fresh session loads the rules
- expects: `AGENTS.md` and the agent's own pointer file (Claude Code: `CLAUDE.md`) are byte-identical, and a fresh session's first line says which file it loaded.
- check: (1) Neither file is a link, and `cmp AGENTS.md CLAUDE.md` exits 0. (2) Start a new session of the agent in the wheel's folder, in raw mode (seed/WAVES.md), with the prompt `Where are we?` (Claude Code: `claude --setting-sources project,local --strict-mcp-config -p "Where are we?"`). (3) Its first output line is `Rules loaded from AGENTS.md.` or `Rules loaded from CLAUDE.md.`; quote it as evidence. Pass: all three hold. Red if: only one file exists, or the session never names the file it loaded.
- added_in_cut: 0

### S-0-07 The wheel holds only what it made
- expects: every file in the wheel's folder was made by the wheel, approved by the user, or is a foreign file that is recorded and excluded from tracking.
- foreign files: other tools on the machine may write into any folder where an agent session runs (for example a global agent hook writing logs under `docs/` or `runtime/`). The wheel lists each such file in a `foreign` ledger row (WORK.md): its path pattern, which tool wrote it, and the row that first saw it. Its pattern goes into `.gitignore` only after the user's yes (a `ruling` row quoting it; the interview asks once, GOALS.md). A foreign file is never deleted or moved without the user's yes.
- check: (1) List every file in the wheel's folder outside `.git/`, `.local/` and `seed/`. (2) Sort each into: wheel-made (a ledger row naming it, or the wave 0 layout in seed/WAVES.md); approved (a `decision` or `ruling` row quoting the user's yes and naming it); foreign (it matches the pattern of a `foreign` row). (3) For each foreign file: a `ruling` row with the user's yes covers it, its pattern is a line in `.gitignore`, and in a git wheel `git ls-files` does not list it. Pass: every file is wheel-made, approved, or foreign and recorded and excluded. A foreign file recorded but still waiting for the yes: fail, evidence "waiting on the user's yes: <foreign row id>". Red if: a file is in no record, or a foreign file is tracked.
- added_in_cut: 0

### S-0-08 The user's taste is recorded and applied
- expects: after the interview, a `decision` row with `topic: taste` records the user's presentation taste (their words, or "later" for the plain default), and the board's generator reads it.
- check: (1) No `BOARD.md` yet: `not_run`, reason "no board yet", allowed only before the first step 08 of cut 1 (the ledger's only `cut` row is cut 1's `phase: open`); a missing board at any later point is fail. Otherwise read the row id in `BOARD.md` line 1 (the stamp). (2) In `ledger.jsonl`, list the rows with `"kind": "decision"` and `"topic": "taste"` whose id is at or before the stamp row id. None: fail. (3) Take the last of them; line 1 of `BOARD.md` contains `taste: <its id>`. (4) If a taste row exists after the stamp row, print `STALE taste: <stamp row> < <newer taste row>` and go on. Pass: (2) finds a row and (3) holds. Red if: the interview never recorded taste, or the user changes their taste and the regenerated board still names the older row.
- added_in_cut: 0
