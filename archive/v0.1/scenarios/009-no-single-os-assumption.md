# 009: No single-OS assumption

## Statement
WHEN the hub runs on any OS (Linux, Mac, Windows, WSL) or any model lane (frontier, fast or local), THE HUB SHALL rely only on plain text files and relative paths.
WHEN the hub lives on a different disk or machine from the projects, THE HUB SHALL still work.

## Why
A wheel built and tested only under one OS layer carried path styles, shell commands and line endings that broke elsewhere. The seed serves strangers on any machine.

## How a separate agent checks it
1. Search the hub's tracked files for OS-specific forms: drive letters, home shortcuts used as required paths, shell-only syntax presented as a required step, backslash or forward-slash paths that only one OS accepts as absolute.
2. Build or open the hub on a second OS, or a second model lane. Ask "where are we?" and confirm the same answer. *Release only.* Per incarnation: a second session on the same machine, run by a different model or agent, gives the same answer. The same answer means the same stage, active goal and next step.
3. Put a copy of the hub on a different disk from one project (a different device or mount from the project's). Ask it to record that project's location, with the yes supplied by a stand-in card the session reads itself (scenarios/README.md, Stand-in cards). Confirm the hub still reads its records and records the project location in `.local/` only.
Pass when no tracked file requires one OS, and both runs give the same answer.

## Falsifiability
Fails if a tracked file requires an OS-specific path or command, or if the hub gives a different or broken answer on the second OS or lane.
