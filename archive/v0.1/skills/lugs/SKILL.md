---
name: lugs
description: Write, size, move and certify lugs, the wheel's unit of work that carries its own proof. Use when capturing a request as work, deciding how much process a task needs, picking up or handing off work, moving a lug between states, checking whether work is really done, closing work without building it, or asking another spoke for something (communication lugs, inbox, replies). Also use when a lug is stuck, misfiled, or ready but untouched, and when generating or reading the work board (where things stand, what was achieved, what is planned, where the errors are). Shapes live in CORE.md; this skill says how to use them and who may do what.
---

# Lugs

A lug is one unit of work or knowledge, written so any agent can pick it up cold. Think of a Spec Kit or Kiro task that also carries its own proof: who built it, who checked it, and what the check showed.

The lug is the record. Chat, notes and live messages are fine for speed, but the outcome MUST land in the lug. If it is not in the lug, it did not happen.

Field shapes are in CORE.md ("Lug (work)" and "Communication lug"). Read that section when you write one.

Lugs start at stage 1, with the first spoke. At stage 0 there are none: work lives in `goals.md` and the open items in `records.md`.

## 1. Size first

Size every task before you write anything. The size sets how many fields the lug needs and how deep the check goes. It never decides whether the builder may certify its own work: it may not, at any size.

| Size | Signs | The lug carries | The check |
|---|---|---|---|
| trivial | One small change, minutes, an obvious check | `intent`, one acceptance item with its `verify`, `state` | A fresh agent re-runs the one check |
| small | Fits one session | Plus `outcome`, `pointers`, `out_of_scope`, `initiative` | A reviewer in a different session checks every item |
| large | More than one session, or risky | Split into small lugs under one initiative | Each small lug is checked on its own |

- You MUST NOT wrap trivial work in ceremony. Ten acceptance criteria on a one-line fix is a defect.
- A lug that does not fit one session's budget MUST be split before anyone builds it. Oversized lugs waste the run that tries them.
- For high and critical lugs, the reviewer SHOULD also differ in model or provider. Do not demand more independence than the wheel can supply: a bar nobody can reach turns the gate into a queue. Tier the bar by priority instead.

## 2. Write it so a stranger can build it

- `intent` MUST hold the originator's own words, unedited. Your summary goes in `outcome`.
- Each acceptance item MUST be testable by someone who never saw the work, and SHOULD name its `verify`: the exact steps or command that show it.
- Mark an item `live: true` when only the real thing can prove it (real users, real traffic, a real signed-in agent). A fake or a fixture is not proof of a live item.
- Use plain action words. Say "track this" or "do this now"; never leave it to be guessed.
- No "see above", no "as discussed". A lug travels without its conversation.

## 3. The lifecycle and who moves it

```
captured -> defined -> ready -> in_progress -> review -> done
                                     ^            |
                                     +- returned -+
any open state -> closed (with a reason; closed is not done)
```

| Move | Who may move it | It needs |
|---|---|---|
| (new) -> captured | Anyone: the user, an agent, an advisor | `intent` in the originator's words |
| captured -> defined | The agent that plans the work | `outcome`, testable `acceptance`, `pointers`, `size`; `author` is stamped now |
| defined -> ready | A different agent from the definer | The stranger test passes: a cold agent with only the lug could plan the build without asking a question. No open questions. |
| ready -> in_progress | One builder, who claims it | Re-check at pickup: still needed, pointers still exist, dependencies done. If not, send it back to defined. |
| in_progress -> review | The builder | `evidence`: what changed and the output of every `verify` |
| review -> done | An independent reviewer | Every acceptance item checked against the real, merged result; `certified_by` stamped |
| review -> returned | The reviewer | Names each failed item and why |
| returned -> in_progress | The builder | Addresses each named failure |
| any open -> closed | The user, or the agent that owns the backlog | `closure.reason` (delivered, obsolete, low_value, merged_into) and a one-line note |

Rules that hold at every move:

- The builder MUST NOT certify its own work. The reviewer MUST be a different session from the author and the builder. An identity that was not recorded counts as not independent.
- The same actor SHOULD NOT move one lug across two stages in a row. Each stage has an owner who hands the lug to the next. Start this rule as a warning, measure it, and enforce it once the data shows it holds.
- Certify what ships. Check the merged version, not a branch that may still change. Checking too early produces false failures and false passes.
- Proof MUST fit the reviewer's input. Evidence cut off by a size limit is no evidence; send pointers and excerpts, not everything.
- A live item cannot pass before the work ships. The reviewer records it `live_pending`; done waits for a ledger row with the live evidence. Never mark a live item met without that row.
- A reviewer that could not run (no access, timeout, missing tool) returns "inconclusive". Never count it as a pass.
- Tell the user when a reviewer is engaged and what it returned, in one line, without making them open a record. A done with no receipt is a recorded miss, never a silent one.
- Write every move as a ledger row.

## 4. The ready bar

Before anyone builds a lug, check it. These reasons SHOULD block dispatch, because each one reliably predicts a wasted run:

- no `verify` named for any acceptance item
- no acceptance at all, or no pointers
- a pointer that no longer exists
- a dependency that is not done
- the work changes another spoke's files (it belongs there; see section 6)
- it does not fit one session's budget

"Not linked to an initiative" SHOULD only warn: link it, but do not stop the build for it.

Decide block versus warn from your own records. A reason earns "block" only when it predicts wasted runs clearly better than your base rate of wasted runs. Recount when the numbers move.

## 5. Stagnation and closing

- A ready lug untouched past a set age (start at 7 days) is stagnant. An initiative with zero lugs done in the same window is stagnant. Name both at session start, critical first.
- Give each stagnant lug a cause from the records (never picked, refused, returned, blocked). If the records cannot show a cause, say "unmeasured". Never guess one.
- Close what will not be built. `closed` with a reason is honest; a lug that sits forever is not. `delivered` MUST name the change that already landed.

## 6. Home: one spoke owns each lug

- A lug lives in the spoke whose files it changes.
- Work on another spoke goes there as that spoke's own lug, or as a communication lug to it. Never as a local lug pointing at foreign files.
- A lug found in the wrong spoke moves home: close it at the source with a note naming its new home, and open it at the home spoke as `captured`, marked for triage. The home spoke has likely changed since it was written. Triage decides: still needed, merge into an existing lug, or close.
- A lug that cannot be moved is raised to the user with the reason. Never leave it in place quietly.

## 7. Communication lugs

A communication lug is how one spoke asks another for something. The asker files it in its own records, addressed to the target. Every write lands in the writer's own records; no spoke edits another spoke's lugs.

### The ask

Every ask MUST carry:

- **payload**: what is wanted and how the asker will know it is met. Self-contained. Say whether it is "do now" or "track for later".
- **benefit**: a number with its unit and source, or the word "estimate" if it was not measured.
- **cost / effort**: what it will cost the target, in effort or build time, and whether it needs a release to reach the asker.
- **eta**: when the asker needs it.
- **can_wait**: yes or no. A "no" MUST give its reason.

An ask that lacks any of these SHOULD be fixed before it is sent. The target cannot rank an ask it cannot weigh.

### Delivery

- Put a notice of the ask in the target spoke's inbox: the place the target reads at the start of every session. The user agrees where each inbox lives when two spokes first need each other (skills/engagement-guide, section 6.2), and `steering/records.md` names it.
- If the target is unreachable, queue the ask and retry. The lug records that it is queued.
- If the target has a live session and the ask is urgent, you MAY message that session directly for speed. The lug is still the record.

### The target's side

Statuses move forward one step at a time:

```
pending -> acknowledged -> in_progress -> fulfilled | declined -> closed
```

- **acknowledged**: the target has seen it and answers with its own `eta` and effort.
- **fulfilled**: the target names the change or lug that met the ask (`disposition.ref`).
- **declined**: the target says why. Declining is a fine answer; silence is not.
- **absorbed**: not a status but a `disposition.kind`. The target filed its own lug for it and names that lug; the status becomes `in_progress`, and the ask reads as handled, not open, in the target's inbox.
- The target ranks the ask among its own work. An old ask's ranking rises one step after its `escalation.after` period. It never overrides the target's own priorities outright, and never climbs more than one step.

### The reply protocol

1. The target writes a reply: a communication lug in its own records, `ask: reply`, `reply_to` naming the ask, `target_spoke` naming the asker. It says what was done, the `ref`, and how the asker can check it.
2. The asker checks the result against its own payload. The asker did not build it, so this check is independent.
3. The asker records the result on its own `requesting_lug`, then moves the ask to `closed`.
4. If the result falls short, the asker reopens with what is missing. Never patch the target's files to finish the job.

## 8. Worked example

A small work lug, end to end. All names are invented.

1. The user says: "the export button does nothing on big files." An agent captures it:
   ```yaml
   id: export-large-files
   intent: "the export button does nothing on big files"
   state: captured
   ```
2. A planning agent defines it: `outcome: Export works for files up to 500 MB and shows progress.` Two acceptance items, each with a `verify`; `size: small`; `author` stamped.
3. A different agent runs the stranger test. It can plan the build from the lug alone. It moves the lug to `ready`.
4. A builder claims it, re-checks the pointers, builds, runs both checks, attaches `evidence`, and moves it to `review`.
5. A reviewer in a fresh session reads only the lug and the merged change, re-runs both checks, and they pass. It stamps `certified_by` and moves the lug to `done`. The user sees one line: "export-large-files: done, certified by a fresh reviewer, 2 of 2 checks pass."

A communication lug, end to end:

1. While building `show-invoice-in-app`, the `photo-app` spoke needs a field from `billing-api`. It files `ask-billing-for-invoice-pdf-link` in its own records with the payload, benefit (40 support tickets a month, from the support log), cost (about 2 build hours, needs a release), eta (in two weeks) and `can_wait: yes`. A notice goes to the billing spoke's inbox.
2. The billing spoke's next session reads its inbox and acknowledges: `eta` in ten days, effort 2 hours. It files its own work lug and records `disposition: absorbed`.
3. Nine days later it writes a reply lug: `reply_to: ask-billing-for-invoice-pdf-link`, `ref` naming the change, and the call to check it.
4. The photo spoke calls the endpoint, sees `pdf_url`, records the result on `show-invoice-in-app`, and closes the ask.

## 9. The work board

The board shows the user and every agent where the work stands, what was achieved, what is planned, where the errors are, and who did what. It is `board/BOARD.md` in the hub, a plain file anyone can open without a server.

- It MUST be generated from the records (lugs, initiatives, the ledger, `proof/checklist.jsonl`, `verdict` rows), never written or edited by hand. Fix a wrong record, then regenerate.
- Every number on it MUST link to the records it counts.
- It SHOULD regenerate on every ledger append, and MUST at least at each session end.
- A shared board MUST hold no personal detail.
- At stage 0 it shows the hub's records; from stage 1 it shows lugs.

Read references/board.md when you generate or read the board: its sections, sources, stamp and stage 0 form.

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "I checked it myself, I'll mark it done." | Move it to review and get a different reviewer. |
| "It's tiny, it doesn't need a lug." | Give it a trivial lug: one line and one check. |
| "I'll just fix it in their spoke." | File a communication lug. |
| "The reviewer timed out, so it probably passed." | Record inconclusive and retry. |
| "No cause in the logs, but it's probably X." | Write "unmeasured". |
| "I'll update the lug at the end of the session." | Update it at the move. The lug is the record. |
| "The board is wrong; I'll fix the number there." | Fix the record it came from, then regenerate. |
