<!--
Sync Impact Report (0.3.0)
- Version change: 0.2.1 -> 0.3.0 (MINOR: two principles added, stated by the operator, 2026-11-05)
- Added: VIII. Plan big, build small; IX. Measure it or it does not count.
- Failing evidence for VIII (seed-trials/results/results.jsonl): in every comparable round the smaller model's build of the same seed scored below the larger model's. Gen 1, seed ba894fe: haiku 6/17 scenarios (31/54 expectations), sonnet 8/17 (33/54). Gen 2, seed 63b04f3: haiku 7/17 (43/56), sonnet 10/17 (49/56). Gen 3 (haiku 6/18, sonnet 5/18) is not comparable: its graders had no build transcript (journal/PROOF-BOARD.md). The seed is not yet executable by a small model.
- Failing evidence for IX: the last two levers, 6b1de90 (frozen ruler, START checklist) and 856e6cf (the work board), were pulled with no measure or baseline named first; the trials board reads "Pulled, not measured yet". The gen 1 and gen 2 fixes changed the evals in the same commits, so their movement cannot be told apart from the ruler's. Every builder predicted 14 to 16 and scored 5 to 10 (calibration error +6 to +11): claims made without a measure.
- Failing scenarios: candidates (a) small-model parity and (b) every lever names its measure, in journal/ruler-v2-notes.md; both run red on the evidence above. They join evals.json with ruler v2 (ruler v1 is frozen).
- Updated: CORE.md glossary (lever, measure; model lane), Charter Check questions 8 and 9; journal/ruler-v2-notes.md.
- Already consistent: START.md (order of authority unchanged), scenarios/evals.json (frozen, untouched).
- Follow-up: Ratified date pending the first signed release.

Sync Impact Report (0.2.1)
- Version change: 0.2.0 -> 0.2.1 (PATCH: wording only, meaning unchanged; exempt from the failing-scenario rule per Governance)
- Modified: IV. The governor. The boundary list gains `time`, matching the governor skill, CORE.md and mandates.md (seven kinds).
- Already consistent: skills/governor, CORE.md glossary, hub/steering/mandates.md

Sync Impact Report (0.2.0)
- Version change: 0.1.1 -> 0.2.0 (MINOR: amendment rule clarified by the operator, 2026-11-05)
- Modified: III. The scientific method; Governance. PATCH amendments (wording only) are exempt from the failing-scenario rule; MAJOR and MINOR still require one.
- Failing case: the 0.1.1 PATCH could not satisfy the old rule (no scenario could run red for a pure clarification).

Sync Impact Report (0.1.1)
- Version change: 0.1.0 -> 0.1.1 (PATCH: clarification, no principle added or removed)
- Modified principles: V. Records travel, code is disposable; VII. Converge the evidence, never the code
- Change: states the split. Shared records (steering files, ledger) travel and are tracked; machine and identity facts live in an untracked .local/ and are re-asked on each machine.
- Failing scenario: none run red; raised from builder feedback that 005 (no personal detail in tracked files) and 014 (rebuildable from the seed) read as conflicting
- Already consistent: START.md, hub/DESIGN.md (R9, R10, R15, .local/)
- Follow-up: Ratified date pending the first signed release
-->
# Wheelwright Charter

Wheelwright reads what you already have (your code, your history, your tools) and tells you plainly what matters and what doesn't. Together we plan where you want to go, and we build only the framework that stage needs: as small as a hobby, as big as an enterprise, always yours. Your hub is the brain beside you. It runs the experiments, keeps the evidence, and advises from what it has measured, learning from every wheel in the fleet so the next wheel rolls better.

## Core Principles

### I. The user's mandates win
Every wheel MUST obey its user's stated mandates over this seed. The wheel MUST discover the user's shop before changing it, and MUST change it in the smallest reversible way.

### II. Done means proven
Nothing is done until it is proven on the real thing. The agent that did the work MUST NOT certify it; a separate agent checks it against scenarios.

### III. The scientific method
Building is a hypothesis, rolling is the experiment, records are the measurement. A MAJOR or MINOR change to this Charter MUST start from a failing scenario; a PATCH (wording only, meaning unchanged) is exempt but still records a sync impact note. Every change forecasts its lift and is measured afterward.

### IV. The governor
Boundaries (spend, time, load, scope, autonomy, risk, privacy) are written down with who set them and why. The wheel works as close to its limits as is safe and never past them. The governed MUST NOT move its own governor: tightening may be immediate; loosening needs the user's yes plus evidence.

### V. Records travel, code is disposable
Records, mandates and taste MUST survive every migration. Shared records (the hub's steering files and the ledger) travel with the wheel and are tracked. Implementations may be scrapped and rebuilt. A wheel MUST be rebuildable from this seed and its shared records.

### VI. Layers are managed
Each layer keeps its memory lean and dated, and carries health signals (cost per use, queue growth, staleness, workarounds, ignored rules). A layer past its signal MUST raise a change nomination.

### VII. Converge the evidence, never the code
Different agents build different wheels by design. Shared vocabulary and record shapes make them comparable. Only results the user chooses to share leave the wheel, and no personal detail is ever in shared files. Machine and identity facts MUST live in an untracked `.local/`; they never travel, and are re-asked on each machine.

### VIII. Plan big, build small
Plans, specs and lugs are written by a capable model and MUST be executable by a smaller, cheaper, faster one without further reasoning. A step a small model cannot carry out is a defect in the plan, fixed in the plan first.

### IX. Measure it or it does not count
Every change, lever and claim MUST name its measure and baseline before it is made, and its movement is shown afterward. An unmeasured change cannot be evaluated, evolved or reported as impact.

## Governance
Amendments follow semantic versioning: MAJOR removes or redefines a principle, MINOR adds one, PATCH rewords without changing meaning. MAJOR and MINOR amendments name their failing scenario; PATCH amendments are exempt from that. Every amendment records a sync impact note and is released signed. Users pin a release and read it before their agent does.

**Version** 0.3.0 | **Ratified** pending | **Last Amended** 2026-11-05
