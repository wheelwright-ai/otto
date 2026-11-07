# GOALS

Template. The wheel keeps its own `GOALS.md`, made from the block below. Goals are the alignment (Charter I): every cut starts here, and every work item names one of these ids.

## Rules
- A goal is the user's own words plus a measure that says when it is met. Write the words unedited.
- A measure has `metric`, `baseline` (read before work starts, or `null` with the cut that will read it), `target` and `source`.
- Goals change often. Every change is a revision: the next `rev` number, a line in the history below and a ledger row of kind `goal` with the reason and the user's words. Revisions are normal; a stale goal is not.
- Never delete a goal. Mark it `met`, `paused` or `dropped`, with the revision that did it.
- Only the user adds, revises or drops a goal. The wheel proposes (START step 09); the user's yes is quoted in the row.
- No personal detail: write "the user", never a name.

## The interview
The first cut opens with it (START step 01), and any cut with no active goal runs it again. Be a specialist, not a form: listen, reflect back what you heard, and help the user find their goals and direction before anything is built. Ask a few questions at a time, never a list. "Later" is a valid answer: record it and move on.

Cover, in this order, and come back to anything left at "later":
1. **Goals.** What the user wants, in their words, and a measure that says when it is met (the rules above).
2. **Direction.** Where they want this to go, and what success looks like to them.
3. **Budget.** The money, time and effort they will spend. Each is a boundary the wheel never moves on its own; only the user's yes moves it (Charter IV).
4. **Seeing progress.** Just in time: what counts as meaningful enough to be told (a seal, a red check, a goal moving, a budget boundary near) and where to be told. On demand: the board, any time they ask.
5. **Taste.** How they want what they see to look and read (BOARD.md, Design craft). "Later" here means the plain default, recorded as such.

Ask once, too, at a natural point: other tools on the machine (for example a global agent hook) may write files into the wheel's folder; may the wheel keep such tool output out of tracking (`.gitignore`) when it appears? It is still recorded and never deleted without a yes (smoke S-0-07). In the same question, tell the user what the first cut's survey found among their global installs (`foreign` rows): the wheel runs raw, sets them aside and changes none of them (WAVES.md).

Every answer is one ledger row quoting the user's words (WORK.md), with a `topic`:
- goals: kind `goal`, `topic: goal`, and the goal written below.
- direction: kind `decision`, `topic: direction`.
- budget: kind `ruling`, `topic: budget`, one row per boundary (money, time, effort).
- seeing progress: kind `decision`, `topic: progress`.
- taste: kind `decision`, `topic: taste` (smoke S-0-08).
- foreign tool output: kind `ruling`, `topic: foreign`.

On the first cut the wheel's folder does not exist yet: hold the answers in scratch, and after the user's yes write them, unedited, as the rows right after the `cut` open row.

After the interview the wheel automates and iterates cut by cut inside those boundaries, telling the user just in time and showing the board on demand. A changed answer is a new row; the latest of each topic wins.

## Template

```markdown
# Goals (rev 1)

## Active
- id: G-001
  words: "<the user's own words>"
  measure: {metric: <what is counted>, baseline: null, target: <value>, source: <where it is read>}
  status: active          # active | met | paused | dropped
  since: rev 1
  review_by: <date>       # when the wheel reads the measure again

## Direction
- "<the user's words>" (row: r-000003)

## Budget (boundaries the wheel never moves on its own)
- money: "<the user's words>" (row: r-000004)
- time: "<the user's words>" (row: r-000005)
- effort: "<the user's words>" (row: r-000006)

## Met, paused or dropped
- (none yet)

## Revision history
- rev 1 | <clock> | added G-001 | reason: first cut | words: "<quote>" | row: r-000002
```
