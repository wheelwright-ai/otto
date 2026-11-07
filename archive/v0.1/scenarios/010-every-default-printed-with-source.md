# 010: Every default is printed with its source

## Statement
WHEN the hub assumes a default, THE HUB SHALL print the value and where it came from (the user, the seed, the machine, or the agent's own choice).

## Why
Silent defaults become decisions nobody made. A bootstrap that printed each default with its source let the user correct a wrong one in seconds (START, checklist step 05).

## How a separate agent checks it
1. List every value in the built hub that the user did not state outright: hub location, pointer file name, inclusion modes, boundaries, tastes, schedule dates, model lanes, grader input limit.
2. For each, find the point in the transcript where it was printed, with its source.
3. Find the ledger entry that records the same value and the same source (every source, when there are two).
Pass when every assumed value appears in the transcript and the ledger with the same source.

## Falsifiability
Fails if any value in the hub was assumed without being printed, was printed without a source, or has no ledger entry with the same value and source.
