Issue: to_unstacked_dataset broken for single-dim variables
Repo: pydata/xarray
SWE-bench run: pydata__xarray-4094

Problem: Converting a Dataset to a stacked DataArray with to_stacked_array followed by to_unstacked_dataset fails when variables are single-dimension (only sample_dims), raising MergeError due to conflicting values for variable 'y'.

Goal: Implement minimal fix so that .to_unstacked_dataset works for datasets where stacked array contains variables that originally had only the stacked sample_dims (single-dim variables). Add targeted unit test and ensure no regressions.

Plan:
1. Triage: locate to_unstacked_dataset implementation path (xarray/core/?) and understand how it merges variables back.
2. Create small tickets: diagnosis, change implementation, add tests, review, QA.
3. Assign Engineer to implement minimal change: when unstacking variables that have only the stacked dimension, ensure coordinate/variable name conflicts are handled — likely avoid merging coordinate "y" as a variable or ensure dims alignment when combining variables.
4. Run tests.

Notes:
- No engineer patch yet. We'll start by assigning the diagnosis ticket.