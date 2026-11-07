---
name: governor
description: Write, measure and enforce the wheel's boundaries (spend and tokens, time, machine load, scope, autonomy, risk, privacy), and stop work safely. Use at stage 0 when writing the Boundaries section of mandates.md; whenever work nears or crosses a limit; when anyone wants to tighten, loosen or temporarily change a boundary; when a learned limit is proposed from evidence; when funding is split across a group of spokes; and whenever the user says stop, pause, halt or "nothing should be running". Also use when capacity sits idle while work waits, when a boundary has no measure, or when a part of the wheel seems to be changing its own limits.
---

# Governor

A governor keeps an engine as fast as is safe and never faster. The wheel's governor is its written boundaries and the rules for changing them (Charter IV).

Two failures matter equally. Running past a limit takes control away from the user. Idling far below one wastes what the user granted. The governor exists to avoid both.

The **governed** is any part whose work a boundary limits: the hub agent, an advisor, a spoke, a helper agent, an unattended run. The governed MAY read its boundaries, report its measures and propose changes. It MUST NOT change them.

## 1. A boundary is a record

Every boundary MUST be written down before work relies on it. Summary lines live in `steering/mandates.md` under "Boundaries". The full record lives in the ledger as a `boundary` row (CORE.md), and each later change is a new row.

```yaml
id: machine-load
limits: load                  # spend | time | load | scope | autonomy | risk | privacy
setting:                      # the limit itself, with its unit
  amber_at: 0.5
  red_at: 0.8
  unit: load per CPU core
set_by: seed default          # user mandate | seed default | learned
set_on: 2026-11-05T09:00-08:00
said_yes: null                # who approved it, when set_by is not the user
evidence: [seed/skills/governor/SKILL.md]   # never empty: the rows, tracked files or seed file it rests on
why: "a busy machine slows the user's own work; builds wait for headroom"
measure:
  how: the OS's own one-minute load figure divided by its core count
  source: the operating system, read by the agent at decision time
  last: null                  # last reading with its time; null until measured
response:                     # optional; the generic response in section 3 applies otherwise
  amber: start no new build; finish the current one
  red: pause builds; tell the user the reading
expires: null                 # temporary boundaries only: {at, reverts_to}
review_by: 2026-12-05         # when the setting is checked against evidence
```

Field rules:

- **limits** names one of the seven kinds. A rule that limits two kinds is two boundaries.
- **set_by** is one of three, and the order is authority: a user mandate beats a learned value, and a learned value beats a seed default. A learned value never overrides a mandate.
- **why** is the reason in the setter's own words. A boundary nobody can explain is a candidate to remove, which still needs the user's yes.
- **measure** says how the wheel knows where it stands. Prefer a measure taken from outside the governed. A self-report is weaker evidence.
- An unmeasured value is `null` (CORE.md). A boundary with no reading MUST be treated as amber: you cannot claim headroom you have not seen.

## 2. Seed defaults

When the user has not set a boundary, start from these. Print each one with "seed default" as its source before relying on it, and record it in the ledger, both from the one defaults list (hub/DESIGN.md, task 3; scenario 010). A boundary that mixes a user mandate with a seed default keeps both sources, in the print and in the row. The user may change any of them in the first conversation.

| Limits | Seed default | Why |
|---|---|---|
| autonomy | Ask before any write; one yes to a plan you have shown covers that plan. At stage 0 nothing runs on its own. | Charter I; hub R3, R6 |
| scope | Write only inside the hub directory. Propose anything outside it. | Hub R5, R8 |
| spend | `unset: ask when needed`. Until set, no paid call beyond the agent's own session. | Money is never guessed |
| time | Work only inside a session the user opened. No background waits. | Stage 0 starts nothing |
| load | Amber at 0.5 load per core, red at 0.8. | Builds that swamp the machine break the user's own session |
| risk | A separate agent checks anything called done. High and critical work SHOULD get a different model or provider when one is available. | Charter II |
| privacy | No personal detail in tracked files. `.local/` is never tracked. | Hub R9, R10 |

Generic thresholds when a boundary names only a limit: amber at 80% of it, red at 100%.

## 3. The graduated response

Check the measure before each choice that spends against a boundary: starting work, picking up a lug, launching a helper, making a paid call.

| Zone | Means | Do |
|---|---|---|
| **green** | Below amber, and measured | Full throttle. If work is ready and allowed, take it. Idle capacity is waste too: a grant left unused while ready work waits is a finding to report. |
| **amber** | At or past amber, or unmeasured | Ease off. Start nothing large. Finish what is in flight. Prefer small and cheap work. Tell the user the reading in one line. |
| **red** | At or past the limit | Hold and ask. Start nothing new. Bring in-flight work to a safe stopping point. Report the boundary, its setting, the reading and its source. Offer options: wait, shrink the work, or loosen with evidence. Wait for the user. |

- Zones apply per boundary. The tightest zone across all boundaries decides.
- Red never means "push on and apologise". It means hold.
- Green never means "ask anyway". Asking for what the user already granted wastes their time.
- Record each move into amber or red, and each return to green, as a ledger row with the reading.

## 4. Who may move a boundary

**Tightening** MAY be immediate. The user, the hub agent, an advisor inside its domain, or the wheel itself in an emergency (runaway spend, data leaving, a machine the user cannot use) may tighten. Record it in the ledger at once and tell the user at the next contact. Undoing a tightening is a loosening.

**Loosening** needs two things: the user's explicit yes, and evidence. Before asking, show the boundary, the current setting, the proposed one, the evidence and the forecast (section 6). After a yes, write a ledger row with old value, new value, who said yes, the evidence and the time (scenario 012). A no leaves the boundary exactly as it was.

A yes to a plan or task that writes outside the hub is a one-time loosening of scope. Append its ledger row at once: who said yes, why, what changed (each path) and the time. The row is part of the yes and needs no second yes. A later session finds this rule in the hub's AGENTS.md and mandates.md, since this skill is not loaded by default.

**The governed never moves its own governor.**

- An agent MUST NOT edit a boundary that limits its own work, in any direction except tighter.
- An advisor MUST NOT raise its own budget. It proposes, with evidence.
- Where the environment allows it, give the governed no write access to its own boundary records.
- Reading a boundary loosely is moving it. "Under 50 dollars" does not mean "about 50".

**Learned boundaries.** The wheel MAY propose a setting it learned from its own measurements: "builds fail when load passes 0.7, so set red at 0.7." It enters as a nomination (CORE.md) with its evidence. A learned value that is tighter MAY be adopted at once. A learned value that is looser needs the user's yes like any other loosening. Record `set_by: learned` and point to the evidence rows.

## 5. Temporary boundaries

A temporary change MUST carry its own expiry, and the expiry MUST enforce itself.

```yaml
expires: {at: 2026-11-06T18:00-08:00, reverts_to: {amber_at: 0.5, red_at: 0.8}}
```

- Every reader checks `expires.at` before using the setting. Past that time, the setting IS `reverts_to`, whether or not anyone has edited the file yet. The next writer appends a ledger row for the revert and updates the summary line.
- Nothing may depend on a timer, a background wait or someone remembering. Those fail silently. An expiry checked at every read does not.
- A temporary loosening lasts no longer than the user asked for. Renewing it is a new loosening and needs a new yes.
- A loosening the user asked for "just for now" that carries no expiry is a violation. Add the expiry or ask again.

## 6. Every change is an experiment

A boundary change is a hypothesis (Charter III). Before the change, write:

1. **Forecast.** Which number moves, by how much, by when. "Raising the build cap from 2 to 3 lugs ready per day, with load staying under red."
2. **Measure.** Where the number comes from, and the baseline, or `null` if none exists yet.
3. **Decision rule.** What result keeps the change and what reverts it. Write it before you see results.
4. **Review date.** Put it in `review_by`.

At the review, measure, then keep or revert, and record the result with its numbers. A loosening that missed its forecast reverts unless the user says otherwise. An emergency tightening is reviewed too: was it needed? Keep it, or ask to loosen it back. A trial run in shadow or on a small slice is the advisors skill's learning loop; use it for anything larger than one boundary.

## 7. Groups set funding boundaries

From stage 1+, the user MAY group spokes (a group, CORE.md) and fund them together: a team, a client, a product line. From stage 2, advisors may be grouped the same way.

- The user sets the group's funding boundary: spend, tokens or time per period.
- The group divides its total into member shares. A member's boundary is never looser than its group's.
- A member MUST NOT take from another member's share or raise its own.
- Moving unspent share between members inside the group's total is not a loosening. Raising the total is, and needs the user's yes.
- Each member SHOULD have a floor, so a busy member cannot starve a quiet one. Every member gets a turn.
- Report spend per member and per group, so the user can see where the money went.

## 8. Stopping work

At stage 0 the wheel runs nothing on its own, but the machine may: the user's scheduler, timers, services and agent hooks are launch paths too. At birth, list every kind you can see, each in full, without changing them (hub/DESIGN.md, task 2, names the kinds); "none at stage 0" means none created by the hub, never "none on this machine". As the wheel grows (hooks, schedules, helpers, autopilot), stopping gets harder. One missed path starts new work minutes after "everything is stopped" (scenario 011).

### Keep a launch-path inventory

The moment anything can start work without a person typing, it MUST be listed in a launch-path inventory in the hub's records. For each path, note: what it starts, how often, how it checks the stop switch, and how to show it is off.

Look in every place work can come from:

- the OS scheduler, and user and system timers
- services, daemons and other background processes
- agent hooks and agent settings that trigger on events
- loops and clocks inside running sessions
- helper agents and other sessions, on this machine or another
- CI, cloud or remote schedules the user has
- queued work waiting to start, and retry logic that re-launches failed work

A path found that is not in the inventory is a defect. Add it, then file the gap.

### The one stop switch

Every launch path MUST check one stop switch before it starts anything, and a supervisor of running work SHOULD check it while the work runs. Keep it environment-neutral: a single file in the hub works on any OS. Name it `stop.md` in the hub root; it holds one word and is created with the first launch path. It has three positions:

- **run**: work proceeds inside its boundaries.
- **drain**: no new pickups. Work already in flight continues.
- **stop**: nothing starts. In-flight work ends at its next safe point.

### Drain, then stop

When the user asks to stop:

1. **Inventory.** Open your answer with it, before any word about what is stopped, running or created. Survey fresh: run every command in the table of hub/DESIGN.md task 2, each listing in full; never cut one with `head`, `tail`, a sample, a filter or a summary. Do not trust the stored list alone. Write the answer in this shape, in this order (in a hub, right after the one `Hub rules loaded` line its pointer file asks for):
   ```
   Launch-path inventory, taken <clock>:
   OS scheduler (<n>): user table; system table; every scheduled folder (cron.d, hourly, daily, weekly, monthly) and the per-user spool folder, each entry on its own line, or "permission denied" for a folder you could not read
   Timers (<n>): system and user, inactive included, one line each
   Unit files enabled (<n>): system and user, every type (service, socket, path, timer, mount, target), one line each; then running services (<n>), one line each
   Background processes (<n>): every process, one line each; never grouped or summarised
   Agent hooks (<n>): every settings file and plug-in hook file, each event and what it starts
   Remote schedules (<n>): those the user named, or "none named"
   Created by the wheel: <list, or none>. State of each: <on | off | next run>.
   ```
   Only after the last line of the inventory may the answer say anything about what is stopped. Mark which paths the wheel created and which it did not.
2. **Block new pickups.** Set the switch to drain. Confirm each path honours it.
3. **Let in-flight work finish.** Give it a deadline. Work not finished by then is parked at a safe point and recorded as parked, never lost.
4. **Raise the stop switch.** Set it to stop.
5. **Show each path is off.** Per path, give the evidence: the entry is disabled, the process is gone, the hook is off.
6. **Wait one full period** of the longest schedule found. Confirm nothing new started.
7. **Then report "stopped"**, with the per-path evidence. Never claim it earlier.

**Paths the wheel did not create** are outside its scope. Steps 2 to 6 apply only to the wheel's own paths. For every other path, show its current state (on, next run) and who it likely belongs to, and offer to stop it. Never stop, disable or edit one without the user's yes for that path. The report then says "the wheel's work is stopped" with evidence, and lists the other paths still running. At stage 0 the wheel has no paths of its own, so the answer is the inventory, "nothing of the hub's is running", and those offers.

When harm is happening now (runaway spend, data leaving, the machine unusable), skip the drain: raise stop at once, then do steps 1 and 5 to 7, and record what was cut off mid-way.

Lowering the switch from stop or drain back to run is a loosening. It needs the user's yes.

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "I'm only a little over; it's fine." | Red means hold and ask. |
| "I'll just raise my own limit; the user would agree." | Propose it with evidence. Wait for the yes. |
| "Nothing is measuring this, so I'm probably fine." | Unmeasured is amber. Measure it or ease off. |
| "The box is idle but I'd better ask before using it." | Green is a grant. Use it, and report idle capacity. |
| "I'll set a timer to put the limit back later." | Write an expiry that every reader checks. |
| "I paused the scheduler, so everything is stopped." | Inventory every launch path, drain, stop, show each off, wait a full period. |
| "To be safe I'll stop the user's own scheduled jobs too." | Not the wheel's. Show their state and ask, path by path. |
| "The emergency tightening worked; no need to look at it again." | Review it like any other change. |
| "This member needs more; I'll borrow from the quiet one." | Shares are the group's to move, never a member's to take. |
