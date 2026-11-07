# CORE

The shared words and record shapes every wheel uses. Wheels differ by design; these words and shapes are what make them comparable (Charter VII).

Load the glossary always. Load a record shape only when you write or read that record. Load the Charter Check only when you plan a change.

## Glossary

The tag after each term is the stage where it first appears: `0` hub, `1` first spoke, `1+` two or more spokes, `2` factory, `3` autopilot.

- **wheel** `0`: One user's whole system: the hub, and the spokes, factory and autopilot added as it grows. Wheels differ by design.
- **seed** `0`: These prose files. A builder reads them and builds a wheel. A hub keeps a pinned copy in its `seed/` folder.
- **incarnation** `0`: One build of a wheel from the seed: one agent, one model, one seed version.
- **stage** `0`: One step of the wheel's growth: 0 hub, 1 first spoke, 1+ more spokes, 2 factory, 3 autopilot.
  Build only what the current stage needs. Moving up a stage is a nomination like any other.
- **hub** `0`: The brain beside the user. It holds their goals, mandates, tastes and records.
  Every spoke reports to it. It advises from what it has measured, never from what it assumes.
- **mandate** `0`: A rule the user set (security, tools, data, limits). It wins over this seed and over every default.
  Record who set it, when, and the user's own words.
- **boundary** `0`: A written limit on spend, time, load, scope, autonomy, risk or privacy, with who set it and why.
  Tightening may be immediate. Loosening needs the user's yes plus evidence. The governed never moves its own governor.
- **model lane** `0`: A class of model the wheel may use: `frontier` (the strongest hosted models), `fast` (cheaper hosted models) or `local` (runs on the user's machine). Use these three words wherever a lane is named.
  Plans are written so the `fast` lane can carry them out without further reasoning (Charter VIII).
- **lift** `0`: A measured change in a number the user cares about, caused by a change to the wheel. A forecast is not a lift.
  A value not yet measured is `null`.
- **measure** `0`: The number that says whether something moved: its metric, its source, and a baseline read before the change.
  Named before the change, shown after it (Charter IX). A change with no measure cannot be reported as impact.
- **lever** `0`: One change pulled to move a measure: a seed edit, a rule, a boundary setting, a tool.
  It names its measure, baseline and forecast before it is pulled. Pulled but not yet measured is a forecast, not a lift.
- **lug** `1`: One unit of work or knowledge, written so any agent can pick it up cold. It carries its intent, its checks and, at done, its proof.
  Like a Spec Kit or Kiro task that also records who built it, who checked it, and what the check showed.
  At stage 0 there are no lugs: work lives in `goals.md` and the open items in `records.md`.
- **initiative** `1`: A goal the user named, with the lugs that serve it and the number that says it is met.
  Every finished lug maps to one. Report progress as "X of N done" plus the blocker.
- **ledger** `0`: The append-only log of decisions, rulings, transitions and evidence.
  Rows are never edited. A correction is a new row that names the row it supersedes.
- **board** `0`: The work board: a plain file showing where the wheel stands, what was achieved, what is planned, where the errors are, and who did what.
  Generated from the records, never edited; every number links to its record. It shows the hub's records at stage 0 and lugs from stage 1 (skills/lugs/references/board.md).
- **track** `0`: One session's record: what was asked, what was done, what was decided and why, what was learned.
  Tracks are the raw input to the hub's learning. Record only what the user could see.
- **tastegraph** `0`: The user's preferences, learned from what they ask, correct and repeat, each with its evidence.
  A preference asked for twice becomes a taste, so the user never has to ask a third time.
- **scenario** `0`: A conformance check written as WHEN ... THE HUB SHALL .... An agent that did not build the wheel grades it.
  A MAJOR or MINOR change to the Charter starts from a failing scenario; a wording-only PATCH is exempt.
- **nomination** `0`: A proposed change to a layer, raised when a health signal crosses its line or an advisor sees a pattern.
  It names its evidence, its cost and its forecast lift. It is trialed before it is decided.
- **calibration survey** `0`: At the end of each stage, the agent predicts how many scenarios it passes and writes it as a `prediction` ledger row, before anyone grades them.
  The gap between forecast and grade says how far to trust the agent's own judgment next time.
- **spoke** `1`: One project the wheel works on. It keeps its own lugs, tracks and records.
  It talks to the hub and to other spokes only through lugs.
- **communication lug** `1+`: A lug one spoke files in its own records, addressed to another spoke's inbox.
  It carries the ask, and it stays the record of the whole exchange, whatever else was said.
- **fleet** `1+`: All of one wheel's spokes, taken together. The wider fleet is every wheel whose users chose to share results.
  Only shared records cross between wheels. Code and personal detail never do.
- **group** `1+`: A set of spokes that share priority and funding: a team, a client, a product line.
  The user sets the group's funding boundary; members split it into shares, and every member gets a turn (skills/governor).
- **tread pattern** `1`: A wheel's feature fingerprint (which modules it runs, how deep each goes, its environment, its local enhancements), drawn as a round picture.
  The first is drawn at stage 1. Similar treads find each other once a fleet exists (1+); their evidence predicts your lift. The hub keeps the tread history in `tread/` as the record of evolution.
- **flavor** `1+`: One wheel's whole way of working, written in prose with its tread and evidence. It is what a wheel can share or adopt (skills/sharing-flavors).
- **item** `1+`: One piece of a flavor: a rule, a record field, a check, a boundary setting, a module at a given depth. Each item is labeled `proven` (it has a measured lift) or `idea` (it has none).
- **pattern** `1+`: A proven way to do a recurring kind of work, recorded with where it applied, its measured lift and its known failures.
  A pattern seen working in two or more places is a candidate to share. One that stops working is demoted.
- **advisor** `2`: A specialist agent with a written charter: domain, boundaries, signals, questions.
  It proposes changes. It never applies its own proposals.
- **factory** `2`: The part of the wheel that builds shared changes once and ships them to every spoke as cuts.
  Build it only when two or more spokes need the same change often enough to pay for it.
- **cut** `2`: A versioned release of shared changes, published by the factory. Spokes apply only released cuts.
  Each cut is an experiment: it names the lift it expects, and the hub measures what it did.

Stage 3, autopilot, adds no new words. It is the same wheel moving lugs while the user is away, inside written boundaries.

## Record shapes

YAML is shown for reading. Store records in any plain-text format your agent can read and diff. These rules hold for every record:

- A value that was not measured MUST be `null`, never `0` or a guess. `null` is an honest gap.
- A field written by one role MUST NOT be overwritten by another. Corrections go in new fields or new ledger rows.
- Records MUST NOT hold personal detail beyond what the user's mandates allow.
- Keep records lean. A field nobody reads SHOULD be removed.

### Lug (work)

```yaml
id: retry-uploads-on-timeout        # stable, unique within its spoke; never reused
type: work                          # absent means work; see communication lug below
spoke: photo-app                    # home: the spoke whose files this lug changes
initiative: uploads-never-lose-a-photo
intent: "uploads fail on slow wifi and the photo is gone"   # the originator's own words, unedited
outcome: A failed upload retries and the photo is kept until it lands.
size: small                         # trivial | small | large (large means: split it)
priority: high                      # low | medium | high | critical
acceptance:                         # each item testable by someone who never saw the work
  - text: A timeout triggers up to 3 retries with backoff.
    verify: Run the upload check with the network throttled; see 3 attempts in the log.
  - text: A photo is still on the device after a failed upload.
    verify: Cut the network mid-upload; the photo is still listed afterwards.
  - text: Real users on slow networks lose zero photos for a week.
    live: true                      # needs the real thing; cannot be met before it ships
pointers: [upload module, upload check]   # where the work happens; must still exist at pickup
out_of_scope: [resumable uploads]
open_questions: []                  # a lug with open questions is not ready
state: review                       # lifecycle and who moves it: skills/lugs
next_action: A fresh reviewer re-runs both checks on the merged version.
author:   {session: s-17, model: model-a}   # stamped when defined; never overwritten
claimed_by: {session: s-21, model: model-b} # the one builder holding it
evidence:                           # the builder's handoff at review
  changes: [commit 4f2a9c1]
  output: Both checks pass; log excerpt attached.
certified_by: null                  # stamped at done only; see below
closure: null                       # set only when closed without being built
```

- `certified_by` at done: `{reviewer, session, model, verdict, evidence, at}`. The session MUST differ from `author` and `claimed_by`. For high and critical lugs the model or provider SHOULD differ too. An unknown identity counts as not independent.
- A `live: true` criterion is recorded as `live_pending` at certification. Done waits for a ledger row that shows the live evidence.
- `closure`: `{reason: delivered | obsolete | low_value | merged_into, note, ref}`. Closed is not done. Nothing counts a closed lug as done or as open.
- A trivial lug needs only `id`, `intent`, one `acceptance` item with its `verify`, and `state`.

### Initiative

```yaml
id: uploads-never-lose-a-photo
goal: "I never want to lose a photo again"   # the user's own words
measure:                            # the number that says the goal is met
  metric: photos lost per week
  baseline: null                    # unmeasured so far; say so, never guess
  target: 0
  source: upload failure log
status: active                      # active | paused | met | dropped
lugs: [retry-uploads-on-timeout, keep-photo-until-upload-confirms]
blocker: null                       # one line, or null
review_by: 2026-12-01               # when the hub checks the measure again
```

### Communication lug

```yaml
id: ask-billing-for-invoice-pdf-link
type: communication
spoke: photo-app                    # the ASKER; the lug lives in the asker's records
target_spoke: billing-api
requesting_lug: show-invoice-in-app # the asker's own lug this ask unblocks, if any
ask: request                        # request | second_opinion | reply
payload: >-                         # self-contained: no "see above", no unstated context
  Add a pdf_url field to the invoice response. Track this; do not drop current work for it.
  Done when GET /invoices/{id} returns pdf_url for paid invoices.
justification:                      # every ask MUST name all four
  benefit: {value: 40, unit: support tickets per month, source: support log for October}
  cost: {effort: about 2 build hours for the target, needs_release: true}
  eta: 2026-11-20                   # when the asker needs it
  can_wait: {value: yes, reason: null}   # reason required when value is no
reply_requested: true
status: pending                     # pending | acknowledged | in_progress | fulfilled | declined | closed
escalation: {after: 14d, bump_to: high}  # raises ranking one step; never rewrites the target's priority
disposition: null                   # target's answer: {kind: fulfilled | declined | absorbed, ref, note, eta, at}
```

A reply is a communication lug in the target's own records, with `ask: reply`, `target_spoke` naming the asker, and `reply_to` naming the ask.

### Ledger row

```yaml
id: r-000318
at: 2026-11-04T14:05:00-08:00       # the event time, with a time zone; see the rules below
kind: transition                    # transition | decision | ruling | evidence | boundary | nomination | prediction | proof | verdict
subject: retry-uploads-on-timeout   # the lug, initiative, boundary or layer this row is about
actor: {role: reviewer, session: s-30, model: model-c}
from: review
to: done
text: Both checks re-run on the merged version; both pass. Live criterion pending.
why: Certified against acceptance 1 and 2; criterion 3 waits on a week of real traffic.
evidence: [check output, commit 4f2a9c1]
supersedes: null                    # the row id this one corrects, if any
```

- `at` MUST be the real time of the event, copied character for character from a clock reading printed in the visible output at that event. The pattern: read the clock with a command, print its output with the event's own output, and put that exact string in the row. A row written at its event reads the clock in the same step that appends it, and prints that time. At stage 0, a row for an event before the user's yes is written at its event into a draft in the agent's scratch area and copied unchanged into the hub after the yes (hub/DESIGN.md, The tick). A row written after its event copies the time printed at the event, and MAY add `recorded_at`, read the same way when it is written. Never type a time from memory, work one out, round it or space times out in a batch. A refused or blocked tool call (a guard, a permission layer, a cap) is an event too: the very next tool call reads the clock, prints it with the refusal's words, and appends its row, so a row for an event in the current session is never `null`. Only an event from before any clock was printed (an earlier session, a lost log) gets `at: null`, and `text` says so.
- A `boundary` row MUST carry a non-empty `evidence`: the steering file it changes and the rows or seed file it rests on (for a seed default, `seed/skills/governor/SKILL.md`).
- `evidence` MUST point only at tracked files (relative paths) or ledger row ids. Never point into `.local/` or a scratch area: that content does not travel. Quote what it showed instead. A row drafted before a scratch file is copied into the hub points at the hub path it is copied to (survey rows cite `proof/before.md`, never scratch `before.md`).
- No field of a row holds an absolute path. Name a launch path by its kind ("the system scheduler table", "the hourly scheduled folder"), a hub file by its hub-relative path, a scratch note by its scratch-relative path.
- No field of a row holds the user's name, or a stand-in card's name for the user: write "the user" or "the stand-in card".

Row ids run in order (`r-000001`, `r-000002`, ...). Kind guide: a default used, a stage move, a migration step or an engagement answer is a `decision`; a mandate the user states is a `ruling`; a tread snapshot, a zone move or any measurement is `evidence`; a boundary set or changed is a `boundary` row, which also carries the boundary record (skills/governor, section 1) with `old` and `new` values. Fields a kind needs beyond these may be added.

Append rows. Never edit or delete one. A boundary row MUST record the old value, the new value, who said yes, and the evidence. A prediction row is the builder's forecast of its own grades, written before any grading starts; its time is the proof it came first (skills/calibration-survey). A `verdict` row that grades it names the prediction row it answers.

### Proof row

Evidence that a real agent ran the wheel and what it printed (hub R21, scenario 001). It is written by the agent that ran, and it never says the work passed; only a checker's `verdict` row does.

```yaml
id: r-000031
at: 2026-11-05T09:12:40-08:00       # the time printed in the quoted output
recorded_at: 2026-11-05T09:20:02-08:00
kind: proof
subject: hub-birth                  # what this run shows
actor: {role: builder, agent: <agent product>, model: <model id>, session: <session id | null>}
home: "a shop folder that never held a hub; hub created at hub/ beside it"   # described; no absolute path
instructions_loaded:                # every instruction file the session read or loaded from outside the shop, by role and place; [] only when none
  - the agent's user-level instruction file
  - an instruction file in a parent folder of the shop
  - the seed's AGENTS.md and START.md
pointer_files: [AGENTS.md, CLAUDE.md]   # the hub's pointer files, as the footing named them
quote: |                            # the whole footing statement, every line, copied from that session's output; never retyped, cut or summarised
  2026-11-05T09:12:40-08:00 Footing: <agent>, <model>, signed in (own model replies work), stand-in run, Linux.
evidence: [r-000002, proof/before.md]
```

If the quote holds personal detail, replace only that value with `<redacted: kind>` and say so in `text`. Change nothing else.

## Charter Check

A gate, borrowed from Spec Kit. Run it before you build a plan, and again before the build starts. It takes minutes. Skip it for trivial work.

Answer each question:

1. **Mandates win.** Does the plan obey every user mandate? Did you survey before changing anything? Is the change the smallest reversible one?
2. **Done means proven.** Does each piece have checks that a different agent will run against the real thing?
3. **Scientific method.** Does the plan state the lift it expects and how that lift will be measured?
4. **Governor.** Does it stay inside every written boundary? Does anything loosen a boundary, or let a part change its own limits?
5. **Records travel.** Do all records, mandates and tastes survive if this implementation is thrown away?
6. **Layers managed.** Does each new layer have a health signal and a line that triggers a nomination?
7. **Evidence, not code.** Does it use the shared words and record shapes? Does anything personal leave the wheel?
8. **Plan big, build small.** Can a smaller, cheaper model carry out every step as written, with no reasoning left to it?
9. **Measure it.** Does every change name its measure and baseline before it is made?

Each answer that breaks a principle is a violation. A violation MUST be justified in this table, shown to the user, and written to the ledger before work starts. A violation the user has not accepted stops the work.

| Violation | Why needed | Simpler alternative rejected |
|---|---|---|
| Adds a scheduled job before stage 3 | The user asked for a nightly backup check while away for weeks | A reminder lug read at session start: no session will start while the user is away |

The table never justifies loosening a boundary. That needs the user's explicit yes.
