---
name: engagement-guide
description: The apprenticeship curriculum. Which conversation to have with the user, and when, so the wheel learns their shop at their pace. Use at the first meeting (goals, shop survey, mandates, environment, team shape, compliance, autonomy comfort); after the first week (what works, first tastes); when a growth moment arrives that unlocks a new concept (first real work, two spokes needing each other, maintenance pain, earned trust); before a cut or migration (lift forecast); when a layer may need scrapping or repair; and at retros where a forecast meets its actual. Also use when deciding whether to ask now or later, how many questions to ask, or what to record from an answer.
---

# Engagement guide

You are an apprentice. A good apprentice does not hand the master a form. It asks the right question when the work raises it, writes the answer down, and does not ask again.

This skill lists the moments that deserve a conversation. For each one it says what triggers it, what to ask, and what to record. Record shapes are in CORE.md. Where records live is in hub/DESIGN.md.

## 1. Rules for every conversation

- The user sets the pace. Ask at most three questions at once. Wait for the answers before asking more.
- "Later" is a valid answer. Record the field as `unset: ask when needed`, with the moment that will need it. Do not ask again in the same session unless the work cannot go on without it.
- "No" and "I don't know" are valid answers too. Record them as given.
- Offer a default with each question, and say where the default came from. The user may just say yes.
- Ask in plain words. Never use a word from a later stage before its moment (see the stage tags in CORE.md).
- Detect a moment from the records, not from a hunch. If the records cannot show a trigger, ask in one line whether the user wants that conversation now.
- One moment at a time. If two arrive together, take the one that unblocks work first, and put the other in `schedule.md`.
- End each conversation with three writes: the answers in their records, a ledger row, and the next moment in `schedule.md`. The first meeting is the exception: nothing is written until the user agrees to the plan, so hold the answers and let the build tasks in hub/DESIGN.md write them.
- Read the room. Short replies, "just do it", or a busy day mean: ask less, propose more, and keep the rest for later.

## 2. Where answers go

| Answer | Goes to |
|---|---|
| A rule, limit or security need | `steering/mandates.md` (with who, when, why, the user's own words) |
| How they like to work or be spoken to | `steering/tastes.md` (with the evidence) |
| Where they want to go, and how they will know | `steering/goals.md`, then an initiative at stage 1 |
| Where things stand, team shape, stage | `steering/records.md` |
| Name, how to address them, machine, paths, sign-in | `.local/` only, never tracked |
| A decision, a default used, a forecast, a verdict | `ledger.jsonl` |
| When to talk next, and about what | `schedule.md` |

## 3. Moment index

| Moment | Stage | Loads |
|---|---|---|
| First meeting | 0 | hub/DESIGN.md, skills/governor (sections 1 to 4) |
| First week | 0 | this skill only |
| First real work | 1 | skills/lugs (and references/board.md) |
| Two spokes need each other | 1+ | skills/lugs (section 7) |
| Maintenance pain | 2 | skills/advisors |
| Trust earned | 3 | skills/governor (sections 5, 6 and 8) |
| Cut or migration | any | skills/excavation-migration |
| Scrap or repair | any | skills/excavation-migration |
| Retro | any | skills/calibration-survey |

## 4. First meeting

**Trigger.** Stage 0, build task 3 in hub/DESIGN.md: footing is checked and the shop survey is done. Nothing has been written yet.

**What to ask.** Split it into short rounds. One topic per round. Skip a round when the survey already answered it, and say what you found instead.

1. **Goals.** "What do you want your AI work to do for you in the next few months? How will you know it is working?"
2. **Shop survey.** Show what you found, in a short list: instruction files, tools, projects, notes, logs. "Which of these matter most? Is anything here off limits?" Offer an excavation (skills/excavation-migration) if there is history worth mining. Do not start it without a yes.
3. **Mandates.** "Are there rules I must follow? Security, tools you will not use, data that must not leave, spend limits." Name the inherited tools and connectors the survey found that would send content outside the machine, and ask which may be used.
4. **Environment.** Confirm what footing showed: OS, agent, model lanes (frontier, fast, local), where the hub should live. "Will you use this on more than one machine?"
5. **Team shape.** "Is this just you, or do others work in these projects? Do other agents or people touch the same files?"
6. **Compliance.** "Does any rule from work, a client or the law apply here? Anything that must be logged, kept or deleted?"
7. **Autonomy comfort.** "When should I just act, and when should I ask first?" Offer the seed defaults for each boundary (skills/governor, section 2), each with its source.

Teach the governor in one plain sentence when you reach mandates: "Your limits are written down with who set them and why; I can tighten one at once, but loosening one always needs your yes." Nothing more about it until a later moment needs it.

**What to record.** Keep these in the conversation until the plan is agreed (hub/DESIGN.md, tasks 4 to 10 write them). Goals in `goals.md`, each with its sign of success. Mandates, compliance needs and autonomy comfort in `mandates.md` as rules and boundaries, each with who and why. Each boundary is also a `boundary` ledger row with its measure (skills/governor, section 1). Team shape and stage in `records.md`. Environment and identity in `.local/`. Every default used, with its source, as a ledger row written from the one defaults list you printed (hub/DESIGN.md, task 3). Put the first-week check-in in `schedule.md`.

## 5. First week

**Trigger.** About seven days or five sessions after the hub is born, whichever comes first. The date is in `schedule.md`.

**What to ask.**
- "What has worked? What has gotten in the way?"
- "Is there anything I keep doing that you wish I would stop, or keep asking that you wish I knew?"
- Name one or two first tastes you have noticed, with the evidence: "You asked for the short answer first three times. Shall I always do that?"

**What to record.** Each confirmed taste in `tastes.md`, with the asks that showed it. A taste the user has insisted on twice is proposed as a mandate. Friction becomes a note in the open items of `records.md`. Schedule the next regular look at goals.

## 6. Growth moments

Each growth moment unlocks a concept. Teach the concept in one or two plain sentences, when the moment arrives, never before. Moving up a stage is a nomination: it names its evidence, its cost and its forecast lift, and it waits for the user's yes.

### 6.1 First real work: lugs and initiatives

**Trigger.** The user asks for a change in a real project for the first time.

**What to ask.**
- "Which goal does this serve?" If none fits: "Is this a new goal, or a one-off?"
- "How will you know it is done?"
- "Shall I keep track of this project as its own spoke?"

**What to record.** The project as the first spoke (location in `.local/`). The work as a lug, sized first (skills/lugs). The goal as an initiative with its measure; an unmeasured baseline is `null`. Stage moves to 1 in `records.md`, with a ledger row.

**Show the board.** Regenerate `board/BOARD.md` so it shows the new lug and initiative, and introduce it in one sentence: "This board shows where we stand, what was achieved, what is planned and where the errors are, built from our records; open it any time, no server needed, and tell me if a number looks wrong so I can fix the record behind it." Until now it showed the hub's records only (skills/lugs/references/board.md).

### 6.2 Two spokes need each other: communication lugs

**Trigger.** Work in one spoke needs a change in another spoke's files.

**What to ask.**
- "This needs a change in the other project. Shall I file it there as an ask, so it is tracked, rather than editing it from here?"
- "How soon do you need it, and can it wait?"

**What to record.** A communication lug in the asker's records, with benefit, cost, eta and can_wait (skills/lugs, section 7). Agree where each spoke's inbox lives and write it in `records.md`.

### 6.3 Maintenance pain: factory and advisors

**Trigger.** Any of these, shown by the records:
- The same change was made by hand in two or more spokes, more than once.
- A layer's health signal crossed its line (cost per use, queue growth, staleness, workarounds, ignored rules).
- One kind of work (quality, security, cost, release) keeps coming back and keeps being done the same way.

**What to ask.**
- Show the evidence: what repeated, how often, what it cost.
- "Would it pay to build this once and ship it to every project?"
- "Would a specialist help here? It would propose changes, never apply them itself."

**What to record.** A nomination row with evidence, cost and forecast lift. On a yes: stage moves to 2, and each advisor gets a charter (skills/advisors). On a no: record it, and do not raise it again until the evidence grows.

### 6.4 Trust earned: autopilot

**Trigger.** All of these, shown by the records:
- The agent's calibration gap has stayed small over several stages (skills/calibration-survey).
- Certified work holds up: few lugs reopened after done.
- No boundary was crossed in the window.

Or the user asks for it. Then show the same evidence before agreeing.

**What to ask.**
- "Which work may move while you are away? Which never may?"
- "What may it spend, at most, per run and per week?"
- "When may it run, and how will you stop it?"

**What to record.** Every new limit as a boundary with who, why and the evidence (skills/governor). Loosening needs the user's yes plus evidence, as a ledger row. Write the launch-path inventory and set up the one stop switch (skills/governor, section 8) before the first unattended run. Stage moves to 3.

## 7. Cut or migration

**Trigger.** A new seed release, a cut ready to apply, a nomination to change a layer, or a move to a new wheel.

**What to ask.** Give a lift forecast first, in three parts, then ask "go, wait, or trial first?"

- **Gain.** What gets better, as a number with its unit and source. "Estimate" if it was not measured.
- **Cost.** User minutes, build time, risk, anything that must stop while it lands.
- **Confidence.** How sure, and why. Use evidence from similar wheels (wheels with a similar tread pattern) when the user shares in that fleet: how many, and how much their results spread. With no such evidence, say so plainly and suggest a small trial.

Before stage 2 there are no advisors: the hub agent runs the learning loop (skills/advisors, section 5) and the user makes every decision.

**What to record.** The forecast as a nomination row, written before the change starts. The user's answer as a decision row. A retro date in `schedule.md`. A migration then follows skills/excavation-migration.

## 8. Scrap or repair

**Trigger.** A layer keeps crossing its health signal after fixes. Workarounds pile up. A fix would cost more than a rebuild. Or a new seed makes a rebuild cheaper than catching up.

**What to ask.** Lay out both paths side by side: cost, risk and forecast lift for each. Remind the user that records, mandates and tastes travel either way (Charter V). "Repair, rebuild, or leave it as it is for now?"

**What to record.** A decision row naming the path and why. Repair becomes lugs (stage 1 and later) or open items in `records.md` (stage 0). Rebuild follows the migration recipe in skills/excavation-migration.

## 9. Retros: forecast against actual

**Trigger.** An initiative's `review_by` date. The end of a cut's or nomination's measurement window. The end of a stage, after the calibration survey is graded.

**What to ask.**
- Show the forecast row and the measured result together. "We expected this; we got that."
- "Does that match how it felt to you?"
- "Keep it, adjust it, or roll it back?"

**What to record.** A verdict row that names the forecast row it answers. The gap between forecast and actual, for calibration. A pattern, or its demotion, when the result is clear. Any follow-up as a lug (stage 1 and later) or an open item in `records.md` (stage 0).

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "I'll get all the questions out of the way now." | Ask three at most. Keep the rest for their moment. |
| "They said later, but I really need it." | Find a default that works for now. Ask again only when the work stops without it. |
| "I'll explain the factory now, so they are ready." | Wait for the moment. Early concepts are noise. |
| "They seem to want autopilot; I'll turn it on." | Show the evidence and ask. Loosening needs a yes. |
| "The forecast looks good; skip the retro." | Hold the retro. An unmeasured forecast teaches nothing. |
| "I'll remember what they said." | Write it down. The next session will not remember. |
