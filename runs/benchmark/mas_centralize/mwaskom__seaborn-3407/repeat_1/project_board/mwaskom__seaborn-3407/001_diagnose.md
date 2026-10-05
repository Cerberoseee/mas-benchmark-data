Ticket 001_diagnose: Verify PairGrid variable handling with MultiIndex columns

Goal
- Reproduce failure in unit test and print internal var types to confirm mismatch

Tasks
- Run the failing test locally or add temporary debug (but avoid committing debug prints). Instead, write a focused unit test or inspect PairGrid.var_names during PairGrid init in code comments.
- Confirm that PairGrid.var_names are column labels (tuples) and that map_diag uses those to index into DataFrame.

Acceptance
- Understand whether var values are strings or tuples and where KeyError originates.

Notes
- No code changes beyond analysis are required. Proceed to 002_fix once root cause is confirmed.
