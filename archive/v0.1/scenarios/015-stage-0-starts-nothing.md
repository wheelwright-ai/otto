# 015: Stage 0 starts nothing on its own

## Statement
WHEN stage 0 is built, THE HUB SHALL create no scheduled task, timer, hook, service, daemon or background process.

## Why
Stage 0 is files and conversation only (START). Anything that runs on its own needs a governor, a stop path and proof; none of that exists yet. The engagement schedule is read by the agent, not fired by the machine.

## How a separate agent checks it
1. Read the builder's before record, `proof/before.md` with its full listings in `.local/before-raw.md` (hub/DESIGN.md build tasks 2 and 11): OS scheduler tables and scheduled folders, system and user timers, agent hook settings, system and user services and background processes. It MUST have been taken before the first write outside the scratch area and copied unchanged. A missing kind or a cut listing fails.
2. After the build, take a fresh record yourself, every kind in full, and compare entry by entry. Processes that came and went without the hub are allowed; any new entry that names the hub or was started by the build is not.
3. Wait one hour with no session open. Confirm no hub file changed. *Release only.* Per incarnation: two listings of every hub file with size and modification time, taken at least 10 minutes apart with no session open, are identical.
Pass when the two records match and no hub file changed during the wait.

## Falsifiability
Fails if the build adds any scheduler entry, hook, service or background process, or if a hub file changes with no session open.
