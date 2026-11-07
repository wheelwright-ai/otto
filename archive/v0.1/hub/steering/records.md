---
inclusion: auto
name: records
description: Load at session start, after any loss of context, and before writing any record.
---
# Records

The page an agent reads to resume work, and the index of where every record lives. Update "Where things stand" at the end of each session. Facts tied to this machine or person go in `.local/`, not here.

## Where things stand
- stage: <0 hub | 1 first spoke | 1+ more spokes | 2 factory | 3 autopilot>
- active goal: <from goals.md>
- next step: <one line>
- open items: <list, or none; include "answers came from a stand-in" when they did>
- last proof: <the latest `proof` row id and the `verdict` that checked it, or "none checked yet">

## Shop
- team shape: <solo | small team | organization> (source)
- projects: listed in `.local/environment.md`

## Where records live
- mandates, tastes, goals: `steering/`
- decisions, defaults, proofs, predictions: `ledger.jsonl`
- check-ins: `schedule.md`
- tread snapshots: `tread/` (from stage 1)
- launch paths: created by the hub: none at stage 0. Already on this machine: <kind and count for every kind in hub/DESIGN.md task 2, e.g. "OS scheduler: 3 entries; system timers: 13; user services: 2 running">, full listings in `.local/before-raw.md`. From the hub's first launch path, the inventory lives here (skills/governor, section 8)
- evidence for graders: `proof/`
- work board: `board/BOARD.md` (generated from these records; never edited)
- tracking: <tool in use | none stated>; `.local/` excluded and `ledger.jsonl` shared, shown in `proof/tracking.md`
- seed version: `seed/PIN.md`
- identity and machine facts: `.local/` (never tracked)

## Fields a later stage needs
Each is filled or marked `unset: ask when needed`. Fields marked "in `.local/`" are filled in `.local/environment.md` under the same name.
- hub location: in `.local/`
- first project: <name | unset: ask when needed>
- first project location: in `.local/`
- os family (linux | mac | windows | wsl | other): in `.local/`
- agent runtime (cli | ide | chat_app | local_runner | other): in `.local/`
- model lanes (any of frontier, fast, local; CORE.md): <value | unset: ask when needed>
- scheduler kind (none | session_only | os_scheduler | ci | cloud): <none at stage 0 | value>
- permission mode: <value | unset: ask when needed>
- grader input limit: <size with unit (source) | seed default 100 KB>
