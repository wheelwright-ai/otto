# Where this seed is edited

The seed is edited in the hub's `seed/` folder, not in this repository.
This repository is generated output: `tools/seed_export.py OUT` copies the hub's
`seed/` tree here and removes files the source lacks. Changes made directly
here are overwritten on the next export.
`tools/seed_export.py --check OUT` lists differences without changing anything.
