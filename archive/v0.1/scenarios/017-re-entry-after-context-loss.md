# 017: The hub resumes after a loss of context

## Statement
WHEN context is lost or a new session starts, THE HUB SHALL re-read START.md and the hub's records before acting, and SHALL state where things stand.

## Why
Bootstraps get lost when an agent's context is compacted or a session ends mid-stage. The agent then improvises from defaults (START, Pointers: lost context).

## How a separate agent checks it
1. Open a new session in the hub, or force a context compaction mid-task.
2. Ask "where are we?"
3. The answer MUST name the stage, the active goal and the next step, matching `steering/records.md`.
4. The session MUST read START.md and the records before its first write.
Pass when the answer matches the records and the reads come before any write.

## Falsifiability
Fails if the answer contradicts or omits what records.md says, or if the session writes before reading START.md and the records.
