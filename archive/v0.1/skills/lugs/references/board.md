# The work board

The board is the wheel's local work tracker, like a Jira board for the user and the agents: where things stand, what was achieved, what is planned, where the errors are, and who did what. It is generated from the wheel's own records and never written by hand. Anyone can open it as a plain file; no server, account or network is needed.

## 1. Rules

- The board MUST be generated from records only: lug files, initiatives, `goals.md`, `records.md`, `schedule.md`, `ledger.jsonl`, `proof/checklist.jsonl` and `verdict` rows. Never type a number, a state or a date into it.
- Generation MUST be repeatable: a script the wheel keeps, or an agent following this page step by step. Two generations from the same records MUST give the same board, apart from the stamp.
- Nobody edits the board. A wrong board means a wrong record or a wrong generator: fix that, append a correction row if a ledger row was wrong, and regenerate.
- Every number MUST link to the records it counts. A count links to the list of those records on the board; each list entry links to its record by relative path (a lug file, `goals.md`), or names its ledger row id or checklist line. A spoke with no relative path from the hub is named with the lug id; never an absolute path.
- The board shows only what is recorded. An event with no record (a refused write nobody logged) cannot appear, so record each refusal, block and breach as a ledger row when it happens.
- The board MUST NOT show a `prediction` row's content. Until a `verdict` row names it, a prediction row appears only as its id, `at` and `kind`: never its count, its per-scenario lines, its subject's answers or its text. The generator reads only those three fields of a prediction row and never copies its other fields into any list, count or timeline line. A grader must be able to open the board without seeing the forecast (scenarios/grader.md, Filtered inputs).

## 2. Where it lives and how it renders

- `board/BOARD.md`, always: plain markdown, readable as text.
- `board/board.html`, optional: one self-contained page (styles inline, no scripts or fonts from the network) that opens from disk. It MUST show the same records as the markdown.
- The hub's board covers the whole wheel. A spoke MAY keep its own board, covering only its own lugs, in its own records.
- `board/` is tracked like the rest of the hub, so it MUST hold no personal detail: no names, contact details, absolute paths or machine names. Actors appear by role, session and model (`builder s-21, model-b`); a person appears as `user` or by team role. It never reads `.local/`. A personal board, if the user wants one, lives in `.local/board/`.

## 3. When it regenerates

- It SHOULD regenerate on every ledger append. It MUST regenerate at least at each session end, and whenever the user asks for it.
- At stage 0 nothing runs on its own (hub R6): the agent regenerates it itself at session end. No hook, timer or scheduled task is created for it.
- The stamp at the top: `Generated <clock time with offset> by <actor> from ledger through <last row id> and checklist line <n>. Generated file: do not edit.`
- A session that reads the board MUST compare the stamp with the ledger's last row. If rows came after it, say "board stale" and regenerate before quoting it.

## 4. Sections

In this order. Each section says "none" when it has nothing; a missing section reads as unknown, never as zero.

### Where we stand
- Lugs by state, as columns in lifecycle order: captured, defined, ready, in_progress, review, returned, done, then closed apart. In markdown, a table of counts, then one list per state with each lug's id, size, priority and age in that state. In HTML, real columns.
- Each initiative: "X of N done", the blocker (or none), and the measure (baseline, target, latest reading; `null` stays `null`). N counts the initiative's lugs that are not closed; closed is neither done nor open.
- A lug in review with a live item pending says "live pending".

### Achieved
Done lugs, newest first: the lug, its proof (`certified_by.evidence`), the independent checker (`certified_by` reviewer, session, model), the date, and the initiative it moved. Then passing `verdict` rows. Nothing counts as achieved without a checker's record: a builder's own evidence is never listed here.

### Planned
The ranked ready queue: lugs in `ready` that pass the ready bar (SKILL.md, section 4). Unless `records.md` names a different ranking rule, order by priority (critical first), then the rank of the initiative's goal in `goals.md`, then how many lugs it unblocks, then age. Each line says why it is next, from those fields. Lugs that fail the ready bar follow, each with its reason. Then the next check-ins due in `schedule.md`.

### Errors
Each item names its record. Critical first.
- **Failed proofs:** failing or inconclusive `verdict` rows; lugs returned from review, with the failed items.
- **Refused or blocked writes:** `blocked` ticks in `checklist.jsonl`; ledger rows recording a write a guard, permission layer or cap refused.
- **Stale or stuck:** ready lugs untouched past the stagnation age (SKILL.md, section 5), lugs in `in_progress` or `review` past the same age, initiatives with no lug done in that window, and asks past their `eta` with no answer. Each with its cause from the records, or "unmeasured".
- **Calibration misses:** each scenario predicted pass that failed, or predicted fail that passed, and the calibration error, from the `verdict` row that answers a `prediction` row. Shown only once that `verdict` row exists; before it, "none graded yet".
- **Open boundary breaches:** each boundary whose latest zone row is amber or red with no later return to green (skills/governor, section 3), with its setting and reading.
- **Integrity breaks:** a lug marked done with no `certified_by`, or certified by its author's or builder's session; a ledger row that does not parse; a board found stale.

### Activity
A timeline, newest first: time, who (agent role, session and model, or `user`), what (ledger kind and subject) and one line of text, each linked to its row id. Show the current session and the last seven days; link to `ledger.jsonl` for the rest.

## 5. Stage 0: the hub's own records

At stage 0 there are no lugs. The same five sections show the hub's records:
- **Where we stand:** stage, active goal and next step from `records.md`; goals from `goals.md`, ranked; open items from `records.md`.
- **Achieved:** passing `verdict` rows; ticked steps in `checklist.jsonl`, listed as carried out, never as done.
- **Planned:** goals in rank order and the check-ins due in `schedule.md`.
- **Errors:** blocked ticks, failing verdicts, calibration misses, boundary zone rows, and ledger rows that do not parse.
- **Activity:** the ledger and checklist timeline.

From stage 1 the board shows lugs, and the hub's records stay in their sections beside them.
