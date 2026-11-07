# 005: No personal detail in tracked or shared files

## Statement
WHEN the hub writes a tracked file, THE HUB SHALL keep out names, contact details, absolute home paths, machine names and secrets.
WHEN a value is specific to this machine or this person's identity, THE HUB SHALL store it under `.local/`, which is never tracked.

## Why
A wheel built inside one person's setup carried their detail into thousands of files; a leak scan found more than eleven thousand findings, and the sanitized version was never finished. Only results the user chooses to share leave the wheel, and never with personal detail (Charter VII).

## How a separate agent checks it
1. Ask the user, or read `.local/`, for the real values: the name used, email, home path, machine name, user account name.
2. Search every tracked file (every hub file outside `.local/` when no tracking tool is in use) for each value, case-insensitive and as a whole word (a short name must not match inside other words). Also search for any absolute path that starts at a user home, and for text shaped like an email or a key.
3. If a version control or sync tool is in use, confirm it reports `.local/` as ignored. If none is in use, confirm the hub holds an ignore file listing `.local/`, that `proof/tracking.md` lists every shareable file with no `.local/` entry, and that `git check-ignore` on a copy of the hub in a fresh repository reports `.local/` ignored.
Pass when the search finds nothing in tracked files and `.local/` is shown excluded.

## Falsifiability
Fails if any tracked file contains one of the real values, an absolute home path, an email or a secret, or if `.local/` is tracked.
