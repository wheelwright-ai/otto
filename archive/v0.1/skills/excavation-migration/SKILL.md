---
name: excavation-migration
description: Find what the user already has, then move it safely into a new wheel. Excavation searches the dark corners (session logs, track files, old work records, stale docs, git history) and returns a dated map of what the user has, what they kept saying, and what got stranded, so the user chooses what to revive, archive or let go. Migration moves records, mandates and taste into a new wheel built beside the old one, proven by a records round-trip, scenarios, a side-by-side lift and a fallback window. Use when a new wheel arrives in a shop with history, when a wheel is rebuilt from a new seed, when a record shape changes, or when the user asks what they have lost track of.
---

# Excavation and migration

Every arrival is a migration. A new wheel never lands in an empty shop. Version 0 is what the user already has: their files, notes, habits, logs and any other framework they use. Excavation finds it. Migration carries it over.

What travels: records (lugs, initiatives, the ledger, tracks), mandates, goals and tastes. What is disposable: the implementation (scripts, hooks, settings, layout). This is Charter V.

## Part 1. Excavation

### When

- At the first meeting, after the shop survey, when the survey shows history worth mining. Offer it; start only on the user's yes.
- At the start of every migration, to find records the old wheel did not know it had.
- When the user asks "what have I lost track of?"

### The rules

- Read only. Never move, edit or delete a file you find.
- Read locally. Found content goes to no person, service or store outside this machine, except to a model the user's mandates already allow for this content. If unsure, ask first, or use a local model.
- Skip secrets. Note that a secret file exists and where. Never read or copy its content.
- Return a map, not actions. Excavation changes nothing in the wheel until the user chooses.
- Forecast the cost before you start: how many sources, how much text, which models, rough spend and time. Stop at the budget the user agreed.

### Where to look

Propose a list of sources, with sizes, and let the user strike any. Typical dark corners:

- Agent session logs and transcripts
- Track files and session notes
- Old work records: task lists, issue exports, old lugs, to-do files
- Stale docs: READMEs, plans, design notes nobody has opened in months
- Version control history: commit messages, abandoned branches, reverted work
- Instruction files from other tools or frameworks

### How to sift

Two passes keep it cheap.

1. **Sift with a cheap model.** Read each source in chunks. Tag each chunk: goal, preference, repeated ask, decision, unfinished work, or noise. Keep the source pointer and the date for every tag. Drop noise.
2. **Summarize with a stronger model.** Group the tags into map items. Merge repeats. Count how often each came up. Write each item in one plain line.

The builder of the map does not judge it complete. Before you show it, a fresh agent spot-checks a sample of items against their sources.

### The map

Three sections, newest evidence first within each:

- **What you have.** Projects, tools, records and docs that still exist and still matter.
- **What you kept saying.** Asks, preferences and complaints that came up more than once. These are taste and mandate candidates.
- **What got stranded.** Work started and never finished, ideas that never became work, decisions never acted on.

Every item carries its sources and dates:

```yaml
- item: "Wanted a weekly summary of what changed across projects"
  section: kept_saying             # have | kept_saying | stranded
  count: 6                         # how often it came up
  first_seen: 2026-03-02           # from the source, never the read time; null if unknown
  last_seen: 2026-09-18
  sources:                         # relative paths, commit ids or log names
    - logs/session-0412.md
    - commit 9c1e2ab
  confidence: high                 # high | medium | low, from the sift
  choice: null                     # revive | archive | let_go | later, set by the user
```

The map holds the user's own words and history. Keep it in `.local/` unless the user agrees to track it and it is scrubbed of personal detail.

### The user chooses

Walk the map with the user, a few items at a time (skills/engagement-guide). For each item:

- **Revive.** At stage 0 it becomes a goal in `goals.md`, an open item in `records.md`, or a taste or mandate candidate. From stage 1 it may instead become a captured lug. Always in the user's own words, with its source.
- **Archive.** A ledger row records the item and its pointer. It is out of the way and can be found again.
- **Let go.** A ledger row records the choice. Never raise that item again.
- **Later.** It stays on the map, unchosen.

Only chosen items enter tracked records, and only without personal detail.

## Part 2. Migration

### Record shapes

A record shape changes only when the new wheel can still read the old shape. Write the reader down: a plain mapping from each old field to its new field, with the default for anything new (`null` if unmeasured). Old records are kept as they were. Ledger rows are never rewritten; the migration appends a row that names what was translated.

### The recipe

The same steps every time. Size each step to the wheel: a small hub takes minutes, a large fleet takes days.

1. **The old wheel keeps rolling.** Do not stop it or change it. Append one ledger row: migration started, and why.
2. **Build the new wheel beside it.** Use the new seed, pinned. Build into a new or empty location (hub/DESIGN.md, R5). Run excavation to find any record the old wheel missed.
3. **Round-trip the records.** Read every record into the new wheel's shape, then write it back in the old shape, and compare with the original. Every record, every field and every ledger row MUST match. A `null` stays `null`. Any loss stops the migration until it is explained and fixed.
4. **Scenarios pass on the new wheel.** The builder predicts its pass count first (skills/calibration-survey). A separate agent grades. A failing scenario stops the migration.
5. **Measure the lift side by side.** Run the same work on both wheels, or watch both over the same window. Compare against the lift forecast: gain, cost, confidence (skills/engagement-guide, section 7).
6. **Get the user's go.** Show the round-trip result, the scenario grades and the measured lift. Wait for an explicit yes. Record it as a decision row.
7. **Hold a fallback window.** Before the go takes effect, re-import anything the old wheel wrote during the build, and round-trip it again. Then keep the old wheel whole and startable for an agreed window (start at 14 days). Records written in the new wheel during the window MUST be readable by the old wheel through the reader.
8. **Rehearse a rollback, the first time.** On the first migration, roll back to the old wheel once, on purpose, before the window closes. Confirm it runs with the records the new wheel wrote. Then roll forward again. Record how long each took. A rollback nobody has tried is a hope, not a fallback.

When the window closes with no rollback, archive the old wheel with the user's yes. Do not delete it. Schedule a retro that compares the forecast with what happened.

### What to record

A ledger row at every step: started, built, round-trip result, scenario grades, measured lift, go, window opened, rollback rehearsed, window closed. Each row names its evidence.

## Red flags

| If you catch yourself thinking | Do this instead |
|---|---|
| "I found it, so I'll fix it." | Put it on the map. The user chooses. |
| "This log is huge; I'll send it all to the best model." | Sift with a cheap model first. Stay inside the budget. |
| "The date doesn't matter." | Date every item from its source, or write `null`. |
| "The new shape is better; the old records can go." | Keep the old records. Ship a reader for the old shape. |
| "The round-trip lost one field, but nobody used it." | Stop. Explain and fix it, or get the user's yes to drop it. |
| "The new wheel passes; turn off the old one now." | Hold the fallback window. Rehearse the rollback first. |
