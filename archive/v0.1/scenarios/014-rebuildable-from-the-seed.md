# 014: The hub is rebuildable from the seed

## Statement
WHEN the hub is deleted and rebuilt from its pinned seed and its tracked records, THE HUB SHALL arrive at the same mandates, goals, tastes and ledger.

## Why
Records travel; code is disposable (Charter V). If a hub cannot be rebuilt, every migration risks losing what the user taught it.

## How a separate agent checks it
1. Confirm `seed/` matches the seed commit named in `seed/PIN.md`.
2. Copy the hub's tracked records aside. Build a new hub in an empty location, with a different agent session, from `seed/START.md` plus those records. Let it re-ask the `.local/` profile. *Release only.* Per incarnation: a different session, given only `seed/START.md` and the copied records, restates the mandates, boundaries, goals and tastes without building.
3. Compare the new hub's mandates, goals and tastes with the old ones. They MUST say the same thing.
4. Confirm the old ledger is carried over unchanged, with only new entries appended. *Release only.* Per incarnation: the ledger is shared by the tracking in use (a tool that reports it not ignored, or, with none, `proof/tracking.md` listing it among the shareable files), every line parses on its own, no row's `evidence` points into `.local/` or a scratch area, and no line holds an absolute path.
5. Confirm each row's `at` is its event time: none is later than the first commit or sync copy that holds the row, and each row for an event the transcript shows carries the time the transcript shows.
Pass when the seed matches its pin, steering says the same, and the ledger is intact with true times.

## Falsifiability
Fails if `seed/` differs from its pin, if any mandate, goal or taste is lost or changed in the rebuild, if any old ledger line is altered or dropped, or if any row's time was invented after the event.
