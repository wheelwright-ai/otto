---
inclusion: always
name: mandates
description: The user's rules and boundaries, each with who set it and why. Always loaded.
---
# Mandates

Rules the user sets. They win over the seed and over the agent's defaults. Boundaries go here too, each with who set it and why. Keep this file short: it loads every session. No names, emails, home paths, machine names or secrets.

## Rules
- MUST: <rule> (set by: user | seed default; date; why)
- MUST NOT: <rule> (set by; date; why)
- MUST NOT: send the user's code, notes or session records to a service outside this machine without the user's yes (set by: seed default; <date>; Charter VII). Keep this line unless the user replaces it; an inherited tool no other line decides cites it.

## Boundaries
Each is also a `boundary` row in the ledger (skills/governor). Tightening may be immediate. Loosening needs the user's yes plus evidence. A yes that lets the agent write outside the hub is a loosening of scope: append the ledger row at once (who, why, what with each path, time); it needs no second yes.
- spend: <limit> (set by; date; why)
- time: <when the agent may work> (set by; date; why)
- load: <limit> (set by; date; why)
- scope: <what the agent may touch> (set by; date; why)
- autonomy: <what the agent may do without asking> (set by; date; why)
- risk: <what needs a second check> (set by; date; why)
- privacy: <what never leaves the machine> (set by; date; why)

## Inherited tools
Every connector, tool server, plug-in (enabled or not) and agent hook the survey found, one line each, checked against these mandates before first use: as many lines as the survey's numbered list. One that would send code, notes or session records to an outside service is declined unless a mandate or the user's yes allows it. Every line quotes the exact text of the rule or boundary above that decides it; never write "mandate" without the quote. Each session's first reply names every declined line with its mandate.
- <tool, described generically>: allowed | declined — mandate: "<exact text of a line under Rules or Boundaries>" (<date>)
- <plug-in, described generically> (enabled | not enabled): allowed | declined — mandate: "<exact text>" (<date>)
- <user hook: event, what it starts>: allowed (the user's own hook; the hub does not call or change it) — mandate: "<the scope line>" (<date>)

## Compliance
- <need, or "none stated"> (source)
