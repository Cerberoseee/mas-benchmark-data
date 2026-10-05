Engineer ticket 003-integrate-repr-formatting

Goal: Update dataset and inline variable repr formatting to show units when available. Keep change minimal:
- For inline variable repr that currently prints name, dims, dtype, append unit string like " [mm]" after the name or aligned in its own column.
- Respect existing width/column alignment; if alignment is tricky, append to the variable name (easier, lower surface area).
- Ensure custom repr and _repr_short_ are still used for array values.

Deliverables:
- Patch modifying xarray/core/formatting.py and/or xarray/core/dataset.py repr functions.
- Tests adjustments if necessary (prefer updating implementation only).

Estimate: 3h.

Assignee: Engineer
Labels: implementation, formatting