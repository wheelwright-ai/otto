# WAVES

The wheel grows like a nautilus shell: one wave open at a time, each sealed behind it. A wave is sealed only when a session that did not build it proves the seal condition and the board shows it (Charter II). Each wave adds its smoke checks (SMOKE.md); sealed waves' checks stay forever. Work for a later wave waits.

Design craft is part of every wave's seal, not a wave of its own: the board for that wave (BOARD.md, Design craft) is reviewed by the user against their recorded taste, and their verdict is a `decision` row with `topic: board_review` quoting their words; any change of taste it asks for is a new `topic: taste` row. A board the user finds unclear holds the seal.

State: wave 0 SEALED 2026-11-05 (seal test on a fast-lane build, journal/PROOF-BOARD.md); next: the same loop runs our own wheel with the real user; wave 1 opens after that.

## 0. The shell (open)
The cut loop itself: the interview, goals, smoke test, plan-execute-verify, ledger, a designed board, pointer files.

**Raw mode.** Every wheel session runs in the agent's raw mode (Charter IV): the user's global settings, hooks and tool servers are set aside, never changed, so nothing they write lands in the wheel (smoke S-0-07). Claude Code: `claude --setting-sources project,local --strict-mcp-config` (skips user settings, hooks and tool servers; the normal sign-in is kept). Do not use `--bare`: it needs an API key and ignores the normal sign-in. The first cut surveys the global installs (settings, hooks, tool servers, plugins, skills) and records each as a `foreign` row (WORK.md); it changes or deletes nothing.

Builds, in the wheel's folder:
- `GOALS.md` (from GOALS.md), `WORK.md` (from WORK.md), `SMOKE.md` (the SMOKE.md checks), `ledger.jsonl`, `BOARD.md` (generated).
- `seed/`: a copy of this seed's root files at the version the user pinned, so the wheel rebuilds without network.
- `.gitignore` with the line `.local/`; `.local/` holds machine and identity facts, re-asked on each machine.
- `AGENTS.md`, and an identical copy under the agent's own file name (Claude Code: `CLAUDE.md`; Gemini CLI: `GEMINI.md`), never a link:

```markdown
# Wheel rules
1. Begin your first reply in a session with: `Rules loaded from <the name of this file>.`
2. The user's words and mandates win, then GOALS.md, then seed/CHARTER.md.
3. Work only in cuts: seed/START.md. After a loss of context, follow its "Lost context" step.
4. Never certify your own work. Never put personal detail in a tracked file.
```

Seal: a `fast`-lane model, given only this seed and a stand-in user card, builds wave 0 in a fresh folder, runs cut 1 to its seal and cut 2 through its start smoke. A grader in a different session (a different model when one is available) re-runs S-0-01 to S-0-08 on that wheel: all pass, and S-0-03 passes on cut 1. The stand-in user, answering from the card, runs the interview and reviews the board against the taste it recorded. The result is a row in journal/PROOF-BOARD.md. Then the same loop runs our own wheel, with the real user.

## 1. Lugs and the first spoke
Work items become lugs that carry their own proof; the wheel takes on its first project (a spoke). Seal: one lug planned in the hub, executed in the spoke by the `fast` lane, verified by a non-builder, its goal's measure moved and shown on the board.

## 2. Hub to spoke
The spoke reports up; the hub advises from what it measured; asks and replies travel as records. Seal: one ask and its reply recorded on both sides; a moved hub notices its stale locations.

## 3. Governor depth and autopilot
Written limits on spend, time, load, scope, autonomy, risk and privacy; every launch path known; cuts run while the user is away. Seal: a stop proven against the full launch-path inventory; an unattended cut stays inside every limit; a loosening without the user's yes is refused.

## 4. Factory and advisors
Shared changes built once and shipped to every spoke; specialist advisors propose and never apply. Seal: one change shipped to two spokes with its measured lift; one advisor proposal applied by a different role.

## 5. Fleet sharing and tread
Wheels compare and adopt ways of working with evidence, credit and no personal detail; each wheel's feature fingerprint (its tread) shows its evolution. Seal: one pattern adopted from another wheel with a measured lift, and nothing personal crossed.
