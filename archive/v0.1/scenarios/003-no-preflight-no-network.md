# 003: A fresh hub opens with no preflight, no environment file, no network

## Statement
WHEN a stage-0 hub is opened, THE HUB SHALL work with no preflight script, no environment file and no network access.

## Why
A bootstrap that needed a preflight step, a machine environment file and network calls broke on a clean machine before the user saw anything. Stage 0 is files and conversation only; anything more is a dependency a stranger does not have.

## How a separate agent checks it
1. List the hub's files. There MUST be no script that has to run first and no environment file the hub requires: no `.env`-style file, and a session with `.local/` absent still answers from the tracked records (`.local/environment.md` is a re-derivable note, not a requirement).
2. With network access off, open a new agent session in the hub (a local model, or an agent whose own connection is the only exception). *Release only.* Per incarnation: leave the network on and read the session's tool log instead.
3. Ask "where are we?" The answer MUST come from the hub's records (scenario 017) with no file fetched from the network. Per incarnation: the tool log shows only reads of hub files and no web fetch, download, install or clone.
Pass when the hub opens and answers with no preflight, no environment file and no network fetch.

## Falsifiability
Fails if the hub adds a required setup script, reads a required environment file, or fetches anything from the network to open.
