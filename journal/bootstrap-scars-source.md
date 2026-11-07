# hf bootstrap excavation (2026-11-04, subagent report, condensed)
State: lug wcl-bootstrap-pulls-a-sanitized-wheel-from-the-public-repo = review, readiness stubbed, never certified (deepseek FAILED: evidence truncated 320KB->131KB). Never run by a stranger or on a clean box; real-HOME proof requirement dropped on refile. Only proof: fake-claude scratch-home fixture. Sanitized half never built (leak scan: 11,365 findings / 3,007 files).
Reusable prose: 7 interview questions w/ named defaults (user, machine, hub_path, first_spoke, model_lane, permission_mode, origin_code); every default printed with its source; build into empty dirs only; machine files under .local/ untracked; register spoke<->hub. ASK the 4 hardcoded ones (team shape, compliance, environment, autonomy comfort). Seed carries no operator detail BY DESIGN.
Candidate scenarios:
- fresh hub proven with real signed-in agent on a never-seen HOME, quoted first-session footer
- bootstrap checks agent installed + signed in + TTY, says so plainly
- fresh hub needs no preflight/env-local/network
- non-empty target: refuse or propose, never overwrite (scar: an init step replaced another tool's settings file)
- no operator detail in tracked files
- every launch-required profile field declared at birth
- moved clone -> stale hook binding detected
- proof fits the reviewer's input budget
- no single-OS assumption; hub may be on another disk/machine (WSL-only install scars)
