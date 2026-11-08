# BOARD

How the wheel's `BOARD.md` is made. The board is where the user and every agent see where the wheel stands. It is generated from the records, never edited by hand.

## Rules
- Regenerate it at START step 08 and again after the seal row (step 10). Between those, a board older than the ledger is stale; say so before quoting it.
- Line 1 is the stamp: the ledger row id and `at` it was generated from, the open or last sealed cut, and the taste row it was rendered with (`taste: r-000007`, or `taste: none` before one is recorded; smoke S-0-08).
- Line 2 is the scope: which wheel and which spokes the numbers cover, and the period.
- Every number links to the records it counts: ledger row ids (`r-000041`) or item and goal ids (`W-003`, `G-001`). A number with no link is a defect.
- Same records in, same board out: no clock reads and no wording that varies between runs, apart from line 1 (smoke S-0-04).
- It never holds personal detail (smoke S-0-05).

## Order (fixed)
1. **Goals.** Each active goal: its id, its metric, baseline -> latest value -> target, and the rows that measured it.
2. **Smoke, start vs end.** For the current or last cut: each check, its start result -> end result, both row ids. A check that went from pass to fail is marked and names its remediation row.
3. **Work through plan, execute, verify.** Counts per state, each with its item ids; then one line per item: id, goal, state, planner lane, and every `verdict` row for it with its result (for example `verdicts: fail r-000032, pass r-000051`), or `verdicts: none yet`. A failed verdict is never left off. From wave 1 the lines are grouped goal, then initiative (computed progress, sign-off), then lugs by rank with kind and status, then the completed history (WORK.md).
4. **Remediations.** Each `remediation` row this cut: the check, what was fixed, the re-run row.

## Design craft
The board is designed, not dumped. These rules hold under every taste:
- Scope line first (line 2), so the reader knows what the numbers cover before reading one.
- Summary before detail: each section opens with one clear headline answer (is the goal moving, did the smoke hold, what is stuck), then the lines behind it.
- Charts where they show movement: burndown, items created vs closed, smoke start vs end, goal progress against target. Each chart carries a one-line takeaway; a chart with nothing moving is left out.
- State is shown by shape and label as well as colour (for example `pass`, `FAIL`, a filled or hollow mark), never colour alone.
- Avoid the generic looks: identical cards, everything centred, decorative gradients, emoji headings. Draw from advanced, effective practice (clear hierarchy, purposeful type and spacing, honest charts), chosen for this user's goals.
- Works in light and dark, and reads on a phone.
- When the taste asks for a rendered page (for example HTML), it is generated from the same records alongside `BOARD.md`, by the same rules.

## Taste
Until the interview records the user's taste (GOALS.md), the default is plain and neutral: headings, short lines, no tables, no colour. The user's taste fixes how it looks (charts, order within a section, symbols, length, medium); record each choice as a `decision` row with `topic: taste` quoting the user's words, and the generator renders with the latest and names it on line 1. Taste never changes what the board counts, the order of the four sections, or the links.

## Delivery
- Just in time: when something meaningful lands (a seal, a red check, a goal moving, a budget boundary near, or what else the user named in the interview), tell the user in one or two lines where they asked to be told, with a link to the board.
- On demand: when the user asks, regenerate the board first, so what they see is always current.
