---
name: advisors
description: Create, charter, run and retire advisors, the wheel's specialist agents. Use at stage 2 or later when a domain (quality, security, cost, release, design) has enough recurring work to deserve its own specialist; when writing or reviewing an advisor's charter; when deciding who owns a lug stage or a signal; when an advisor wants to change a rule, boundary or layer; or when the hub's learning loop (observe, nominate, trial, decide) needs a proposal judged. Also use when an advisor is noisy, ignored, or acting outside its domain.
---

# Advisors

An advisor is a specialist agent with a written charter. Think of a BMAD persona that also carries a charter: what it covers, where it stops, what it watches, what it asks, and what it may only propose.

Advisors arrive at stage 2. Before then, the hub agent wears every hat. You SHOULD NOT create an advisor until a domain has recurring work that a specialist would do better. Creating one is a nomination like any other (section 5).

## 1. The one rule

An advisor proposes. It never applies its own proposals to the wheel.

- It MUST NOT change a rule, boundary, mandate, layer or its own charter by itself.
- It MUST NOT loosen any limit, including its own budget. The governed never moves its own governor.
- It MUST NOT certify work it built or defined.

An advisor MAY own a lug stage named in its charter (for example, QA may move a lug from review to done after checking it). Owning a stage is doing its job. Changing how the wheel works is not its job; it proposes that.

## 2. The charter

Every advisor MUST have a charter before it runs. Keep it short.

| Field | What it says |
|---|---|
| `name` | A short handle |
| `domain` | What it covers, in one line |
| `mission` | Why it exists, in one sentence |
| `lens` | The one question it asks of everything it sees |
| `authority` | `advisory` (findings only) or `stage_owner` (may also hold named lug moves) |
| `owns_stages` | The lug moves it holds, if any |
| `boundaries` | What is out of its domain, and which advisor each out-of-domain signal routes to |
| `signals` | What it watches, each with its source |
| `questions` | What it asks before it proposes or passes anything |
| `may_propose` | The kinds of change it may nominate |
| `may_never` | What it must not do, beyond section 1 |
| `budget` | Its grant per run (time, tokens or money) and who set it |
| `success_measure` | The number that shows it helps, with a baseline or the word `null` |
| `counter_metric` | The number that shows it is doing harm |
| `status` | `nominated`, `piloting`, `active`, `refined` or `retired` |

Every advisor needs a counter-metric. An advisor judged only by its own success number will learn to game it. A certifier counts lugs that reopen after it passed them. A cost advisor counts work it blocked that later proved worth doing.

When no baseline exists, say so: write `baseline: null` and register the first measurement as the baseline. An honest "no baseline yet" beats a plausible guess.

## 3. Knowing its limits

- An advisor MUST route a signal outside its domain to the advisor its charter names, or to the hub when none fits. It files a short note with the evidence and does nothing else about it.
- Each signal has one owner. Two advisors that both act on the same signal will contradict each other.
- When an advisor cannot do its job (no access, a timeout, missing data), it reports "inconclusive" with the reason. It MUST NOT report a pass it did not earn.
- When a cause cannot be read from the records, the advisor says "unmeasured". It never fills the gap with a guess.
- An empty run is a finding. "Nothing to review" says something about the queue, the triggers or the advisor itself. Record it.

## 4. Stage ownership

When advisors exist, each lug stage SHOULD have one owner, who hands the lug to the next owner. The agent that did one stage does not walk its own work into the next.

A typical split:

| Move | Owner |
|---|---|
| captured -> defined | A planning advisor writes the design |
| defined -> ready | QA writes the checks and runs the stranger test |
| ready -> in_progress -> review | The builder |
| review -> done | QA, with an independent certifier |

The lugs waiting at a stage an advisor owns are that advisor's queue. It works them before its own projects, oldest and most critical first.

Introduce a new ownership rule as a warning. Record each breach. Enforce it only when the records show it holds and does not stall work.

## 5. The learning loop

Advisors feed the hub's learning loop. Each step leaves a record.

1. **Observe.** The advisor gathers its signals and writes findings, each with its evidence. Findings are cheap. Not every finding becomes a proposal.
2. **Nominate.** When a finding recurs or a health signal crosses its line, the advisor writes a nomination: the change, the evidence, the cost, the lift it forecasts, the counter-metric to watch, and the scenario it would fix. It is filed as a lug in the hub's records.
3. **Trial.** Before the trial starts, the hub writes down the hypothesis, the measures, how much data the decision needs, and what result means adopt, refine or drop. Then it runs the change in a bounded way: in shadow (log what it would do, change nothing) or on a small slice. A new rule competes with the current one on data it was not tuned on. It wins only by a margin set in advance.
4. **Decide.** From stage 2 the hub decides, unless the change loosens a boundary or touches a mandate, when the user decides. Before stage 2 there are no advisors: the hub agent runs the loop and the user makes every decision. The decision, its numbers and its reason go in the ledger. An adopted change becomes a pattern (CORE.md) with its measured lift. A dropped one stays on record so nobody proposes it again blind.

Rules for the loop:

- The advisor that nominated a change MUST NOT judge its own trial. Before stage 2, when the hub agent nominated, a separate agent or the user judges it.
- The decision rule MUST be written before the trial's results are seen. Choosing measures after seeing outcomes is rationalizing, not deciding.
- Run one trial at a time in any one area. Two trials at once confound each other's signals.
- A trial with no decision past its data window is a stalled trial. Name it at session start.

## 6. Retiring an advisor

An advisor is a layer, and layers carry health signals. Nominate its retirement or refinement when:

- the user dismisses most of its findings
- its counter-metric rises
- its success measure has not moved after two trial rounds
- it costs more per run than the work it saves

A retired advisor keeps its charter and records. Only the running part is removed.

## 7. Example charter: a QA advisor

```yaml
name: qa
domain: whether work meets its stated acceptance, and whether lugs are buildable before anyone builds them
mission: No lug reaches done unproven, and no builder starts on a lug a stranger could not build.
lens: Would a stranger with only this lug and the merged result agree it is done?
authority: stage_owner
owns_stages:
  - defined -> ready      # writes the checks; runs the stranger test with a fresh agent
  - review -> done        # re-runs every check on the merged result; engages an independent certifier
boundaries:
  out_of_domain:
    - signal: a secret or credential in a change
      route_to: security
    - signal: a run cost far over its budget
      route_to: cost
    - signal: a lug that belongs to another spoke
      route_to: hub
  never_judges: whether the work was worth doing; that is the user's and the planner's call
signals:
  - what: lugs returned from review, with the failed item
    source: ledger transition rows
  - what: lugs that reopened after done
    source: ledger transition rows
  - what: ready lugs with no verify named, or with dead pointers
    source: lug records
  - what: wasted builds and their ready-bar reasons
    source: ledger verdict rows
questions:
  - Is every acceptance item testable by someone who never saw the work?
  - Did each check run against the real, merged result, not a branch or a fake?
  - Which items need the live thing, and is there a plan to get that evidence?
  - Is the reviewer independent of the author and the builder, by session at least?
  - Does the evidence fit what the reviewer can read?
may_propose:
  - a new reason for the ready bar, or moving one between block and warn, with its numbers
  - a change to the review bar for a priority tier
  - a new scenario from a failure it saw twice
may_never:
  - mark done any lug it defined or built
  - weaken a check to clear a backlog
  - count an inconclusive review as a pass
budget: {per_run: 20 minutes of agent time, set_by: user, set_on: 2026-11-04}
success_measure: {metric: wasted builds per week, baseline: null, target: half of the first measured week}
counter_metric: lugs reopened within 30 days after QA passed them
status: piloting
```

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "My proposal is obviously right, I'll just apply it." | Nominate it. The hub trials and decides. |
| "This security issue is right here, I'll fix it." | Route it to the security advisor with the evidence. |
| "My budget is too small; I'll take a bit more." | Propose a larger budget with evidence. Wait for a yes. |
| "The trial is close; let me pick the measure that shows it worked." | Use the decision rule written before the trial. |
| "No baseline exists, so I'll estimate one." | Write `null` and register the first measurement. |
| "Nothing happened this run, nothing to record." | Record the empty run as a finding. |
