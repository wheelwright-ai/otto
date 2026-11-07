---
name: tread
description: Draw and use a wheel's tread pattern, its feature fingerprint. A tread records which modules the wheel runs, how deep each goes (hobby, pro, enterprise), its environment profile (OS family, agent runtime, model lanes, scheduler kind), its local enhancements and its measured lifts, and renders them as one round picture. Use when stage 1 begins and the first tread is drawn; at each stage move, migration, cut or adopted change, when a new dated snapshot goes into the hub's tread history; when the user asks what their wheel looks like or how it has evolved; when looking for similar wheels whose evidence can forecast a lift; when asking what similar wheels run that this one does not; and before sharing a flavor or comparing flavors side by side.
---

# Tread

A tire's tread tells you what road it was built for. A wheel's tread does the same: one picture of what the wheel runs, how deep, where, and what each piece has been shown to deliver.

Treads exist so wheels can be compared (Charter VII). Two wheels with similar treads tend to get similar results. So the evidence from wheels like yours is the best forecast of what a change will do for you, short of trying it.

A tread is a record, not a brag. Every depth and every lift in it MUST trace to evidence in the hub's records. A tread drawn from hopes is worse than none.

## 1. When to draw one

- **First tread:** when stage 1 begins (the first spoke). A stage 0 wheel MAY draw one at birth as a baseline.
- **New snapshot:** at each stage move, migration, applied cut, and adopted or dropped nomination that changes a module or an enhancement. Also at each scheduled review in `schedule.md`.
- **On request:** when the user asks what the wheel looks like, or how it changed.

Never edit a past snapshot. A correction is a new snapshot, with a ledger row naming the one it corrects.

## 2. What a tread holds

Copy `assets/tread.yaml`. It has five parts.

### Who and when
- `wheel_label`: a pseudonym the user picks, or two random words. It MUST NOT be a person, company, project or machine name.
- `scope`: `wheel` (the whole wheel), `spoke` (one spoke) or `group` (spokes the user funds together, skills/governor section 7).
- `drawn_at` with its UTC offset, `stage`, and `seed_version` from `seed/PIN.md`.

### Modules
One entry per module, in the fixed order given in the template. A module the wheel does not run is still listed, at depth `none`. Fixed order and fixed length are what let two treads line up.

Modules the wheel invented for itself go after the fixed list, sorted by id, marked `local: true`.

Each module carries its `depth` and the `evidence` for it: a record path or ledger row id.

| Depth | Ring | Means |
|---|---|---|
| none | 0 | Not run. |
| hobby | 1 | Used by hand. Its records exist and are kept. Few or no measures. |
| pro | 2 | Used regularly. It has a health signal that is measured, and its work is checked by a separate agent. |
| enterprise | 3 | Serves several people or groups. Boundaries and funding are set per group, and a third party could follow its audit trail. |

- Depth MUST be the highest level the evidence shows, never the level the wheel is aiming for.
- A depth with no evidence MUST drop to the level below, down to `none`.
- Bigger is not better. A solo user's wheel at hobby depth everywhere can be exactly right. Never present a deeper ring as a goal unless the user's goals ask for it.

### Environment profile
Four fields, each a family, never a specific machine. These make similarity meaningful: a lift on one runtime may not hold on another.

- `os_family`: `linux | mac | windows | wsl | other`
- `agent_runtime`: the kind of agent: `cli | ide | chat_app | local_runner | other`, plus the product family name if the user agrees. No version below major, no account detail.
- `model_lanes`: which lanes the wheel uses: any of `frontier`, `fast` (small and cheap), `local`.
- `scheduler_kind`: what can start work without a person: `none | session_only | os_scheduler | ci | cloud`.

Nothing else goes here. No paths, hostnames, names, emails, team size, employer or client. The full environment lives in `.local/` and never enters a tread.

### Enhancements
A local change the wheel made on top of a module: a rule, a record field, a check, a prompt. Each has an `id`, the `module` it improves, one plain line saying what it does, `since`, and a `lift` id or `null`.

An enhancement with no measured lift is an idea, and is drawn as one (section 3). That is fine. It is a candidate for a trial, not a claim.

### Lifts
A lift is a measured change in a number the user cares about, caused by a module or an enhancement.

- Each lift names its `metric`, `unit`, `direction` (`higher_better | lower_better`), `baseline`, `after`, sample size `n`, `window`, `source`, and the ledger rows that hold the measurements.
- `measured_by` names the role that measured it. A lift measured only by the builder of the change is weak evidence; say so.
- An unmeasured value is `null` (CORE.md), never a guess and never `0`.
- A lift MUST come from a decided trial or a review, not from a forecast. Forecasts live in nominations.

## 3. The rendering rule

The picture MUST be reproducible from the YAML alone, by any agent, on any OS, with no library. Render plain SVG text. The same tread always gives the same picture.

**Canvas.** `viewBox="-180 -130 360 290"`. Center at `0,0`. The wide sides leave room for labels. The caption sits at y = 150.

**Segments.** Let N be the number of modules, fixed list plus local ones. Segment `i` (counting from 0) spans angles `a0 = i * 360 / N` to `a1 = (i + 1) * 360 / N` degrees, measured clockwise from 12 o'clock.

A point at angle `a` and radius `r` is `x = r * sin(a)`, `y = -r * cos(a)`, with `a` in radians for the math. Round to one decimal.

**Rings.** Three circles, radius 30, 60 and 90, for hobby, pro and enterprise. Thin stroke, no fill.

**Spokes.** A thin line from the center to radius 90 at each segment boundary.

**Depth wedge.** For a module at depth d (1 to 3), draw a wedge from the center to radius `R = 30 * d`:

```
M 0 0  L x(a0,R) y(a0,R)  A R R 0 0 1 x(a1,R) y(a1,R)  Z
```

The large-arc flag is `0`: the fixed list keeps every segment far under 180 degrees. A module at depth `none` gets no wedge.

**Fill means evidence.**
- Solid fill: the module has at least one measured lift in this tread.
- Light fill (about 35% opacity): the depth has evidence, but no measured lift yet.
- A local module gets a dashed outline on its wedge, so invented modules stand out.

**Marks are enhancements.** For each enhancement, put a small circle (radius 3) at radius 100, inside its module's segment. Space k marks evenly across the segment: mark j (from 0) sits at angle `a0 + (j + 1) * (a1 - a0) / (k + 1)`. A filled mark has a measured lift. A hollow mark is an idea.

**Labels.** Each module's short id at radius 115, at the segment's middle angle. Anchor the text `start` on the right half, `end` on the left half, `middle` within 10 degrees of top or bottom.

**Caption.** One line under the picture: `wheel_label`, `scope`, `stage`, `drawn_at` date, and the four environment fields.

**Color.** Use `currentColor` for every stroke and fill, so the picture reads in light and dark themes and in print. Meaning MUST NOT depend on color. A user may add a palette; the shapes still carry the meaning. Some standalone SVG converters ignore `currentColor` and draw nothing; when converting to an image outside a page, replace it with one dark color first.

**Text fallback.** Every render ships with a plain table beside it: module, depth, evidence, enhancements, lifts. A reader who cannot see the picture loses nothing.

**Comparing.** Draw treads at the same size, side by side, in the same segment order. For an evolution view, draw a wheel's snapshots oldest to newest, left to right, each captioned with its date.

## 4. Where treads live

- The hub keeps a `tread/` folder. Each snapshot is `tread/<YYYY-MM-DD>.yaml`, with `-2`, `-3` for a second or third on the same day. Its SVG sits beside it with the same name.
- Each snapshot gets an `evidence` ledger row pointing to it.
- Treads hold no personal detail, so they are tracked records and travel with the wheel (Charter V).
- A tread leaves the wheel only when the user shares it, by the rules in skills/sharing-flavors.

## 5. Using a tread

### Find similar wheels
Only possible when the user takes part in a fleet and has incoming treads from pinned, signed releases (skills/sharing-flavors). Never fetch or share treads without the user's yes.

The seed default for similarity, between 0 and 1:

- **Module distance:** the sum, over every module in either tread, of the depth difference in rings, divided by `3 *` that number of modules.
- **Environment distance:** the share of the four environment fields that differ. For `model_lanes`, it counts as differing if the sets do not overlap.
- **Similarity** = `1 - (0.7 * module distance + 0.3 * environment distance)`.

Print this rule with "seed default" as its source the first time you use it (scenario 010). A wheel MAY tune the weights from its own evidence; record the change as a nomination.

Call a wheel similar at 0.75 or above. Report how many similar wheels you found, and the spread of their similarity.

### Forecast a lift from their evidence
For a module or enhancement you are considering:

1. Take the similar wheels that adopted it and measured a lift.
2. Report n, the mean lift weighted by similarity, and the range.
3. With fewer than three, say "too little evidence" and propose a small trial instead of a forecast.

The forecast goes in the nomination before any trial starts. After the trial, compare your measured lift to the forecast. That gap tells the wheel how far to trust fleet evidence next time, the way the calibration survey does for a builder.

### See what similar wheels run that you don't
List each module depth and enhancement that similar wheels have and yours lacks. Rank by how many similar wheels run it times their mean measured lift. Show ideas (no lift) in a separate, lower list.

Each line is a candidate nomination, never an instruction. Something that suits most wheels like yours may still break one of your mandates. Mandates win.

### Show evolution
Read the snapshots in date order. For each step, list modules added or removed, depth changes, enhancements added or dropped, and new lifts. Name the ledger rows that caused each change. A depth that went down is a finding, not a failure: say what happened.

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "We're nearly pro on this; I'll draw it at pro." | Draw the depth the evidence shows. |
| "This enhancement obviously helps; I'll fill its mark." | Filled means measured. Hollow until a trial says so. |
| "I'll leave the unused modules off; the picture is cleaner." | Every fixed module is listed, or treads stop lining up. |
| "The machine name makes the caption clearer." | Families only. Machine and identity facts stay in `.local/`. |
| "Similar wheels all run this; let's add it." | It is a nomination. Forecast, trial, decide. |
| "I'll update last month's snapshot with the fix." | Snapshots are never edited. Draw a new one. |
| "Our lift beat the forecast; the fleet evidence must be wrong." | Record the gap. One trial is one data point. |
