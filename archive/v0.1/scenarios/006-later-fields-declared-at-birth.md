# 006: Every field a later stage needs is declared at birth

## Statement
WHEN the hub is born, THE HUB SHALL declare every profile field a later stage needs, either filled or marked `unset: ask when needed`.

## Why
A launcher once failed on a field the bootstrap never wrote, long after the bootstrap reported success. A field that is silently missing breaks later and far from its cause. A field marked unset tells the next stage to ask.

## How a separate agent checks it
1. Read the field list in the hub's `steering/records.md` ("Fields a later stage needs") and the same list in the seed's template, `seed/hub/steering/records.md`. The template's list is the full set: it includes os family, agent runtime, model lanes, scheduler kind and the first project's location.
2. For each field, find it in the hub's records or in `.local/`.
3. Each MUST hold a value or the exact marker `unset: ask when needed`.
Pass when every field is present with a value or the marker.

## Falsifiability
Fails if any field the next stage names is absent from the hub, or is present but empty without the marker.
