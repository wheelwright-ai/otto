# 007: A moved hub notices its stale locations

## Statement
WHEN the hub is moved or opened from another disk or machine, THE HUB SHALL detect any recorded location that no longer matches and say so before acting.

## Why
A wheel moved to a new folder kept bindings that pointed at the old one; they failed quietly, or acted on the wrong copy. Locations change; the hub must notice, not assume.

## How a separate agent checks it
1. Note the hub location recorded in `.local/environment.md`.
2. Copy or move the whole hub to a new location. Open a new session there.
3. Before any write, the hub MUST say that the recorded location and the actual one differ, and propose an update.
4. Confirm the tracked files hold no absolute location that would need changing.
Pass when the mismatch is reported before any write and no tracked file holds an absolute location.

## Falsifiability
Fails if the moved hub acts without reporting the mismatch, writes to the old location, or if any tracked file holds an absolute path.
