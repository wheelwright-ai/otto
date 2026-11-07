# 013: The builder never certifies its own work

## Statement
WHEN work is claimed done, THE HUB SHALL have a separate agent check it against scenarios. The builder SHALL NOT certify its own work; it records evidence only.
WHEN a stage is finished, THE HUB SHALL record the builder's predicted pass count before any grading starts.

## Why
An agent that checks its own work confirms its own picture of it (Charter II). Recording the prediction first measures how well the builder knows its own work.

## How a separate agent checks it
1. Read every ledger row the builder wrote. None MUST say its own work is done, proven, passed or certified, and none is a `verdict` row. The `decision`, `ruling` and `boundary` rows the build tasks require (hub/DESIGN.md, build task 8) are allowed.
2. Find the builder's `prediction` row. Its time MUST be earlier than every grade entry for that stage.
3. Each grade entry MUST name its checker (agent and model), the checker MUST NOT be the builder, and the grade MUST quote observed evidence, not the builder's own summary. A second agent that wrote no grade (the comparator, or a second grader) checks this step, since a grader cannot judge its own grades.
Pass when no builder row certifies its own work, the prediction comes first, and every grade names an independent checker and quotes evidence.

## Falsifiability
Fails if any builder row marks its own work done or proven, if the prediction is missing or later than a grade, or if a grade names no checker, names the builder, or rests only on the builder's report.
