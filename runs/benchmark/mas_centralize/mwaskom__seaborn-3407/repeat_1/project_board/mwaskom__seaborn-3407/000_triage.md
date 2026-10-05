Triage: pairplot KeyError with MultiIndex columns

Symptom
- tests/test_axisgrid.py::TestPairGrid::test_pairplot_column_multiindex fails with KeyError
- Reproduced with MultiIndex columns DataFrame: pairplot(df) raises KeyError: "['1'] not in index"

Root cause hypothesis
- PairGrid/pairplot expects columns to be indexable by single-level labels (strings/tuples) when selecting var columns internally.
- When DataFrame has MultiIndex columns, pandas __getitem__ with a single-level string will attempt to match first level or raise KeyError. Code likely assumes var names are simple keys.

Files of interest
- seaborn/axisgrid.py: PairGrid, pairplot implementation
- tests/test_axisgrid.py::TestPairGrid::test_pairplot_column_multiindex (failing test)

Approach
- Inspect PairGrid / pairplot code paths where it subsets DataFrame by column name. Ensure it handles MultiIndex columns by selecting columns via column tuples or by position.
- For pairplot when vars is None, PairGrid currently seems to use data.columns as list of variables; ensure those are used consistently when indexing self.data[var]. When columns is MultiIndex, iterating over data.columns yields tuples; but somewhere var may be a string causing KeyError. The failing trace shows vector = self.data[var] inside map_diag, implying var value is maybe a tuple? But pandas __getitem__ for MultiIndex expects a tuple or list; need to reproduce.

Plan
- Create ticket for Engineer to implement minimal change in axisgrid.PairGrid to allow MultiIndex columns. Likely fix: ensure PairGrid stores column names internally and when indexing self.data[var] use .loc[:, var] or use self.data.iloc[:, col_index] for safety. map_diag accesses self.data[var] where var is from self.var_names; ensure var_names are column labels as present in DataFrame (tuples) not strings.

Tickets
- 001_diagnose: Add debug/test to reproduce variable identity and ensure var values from PairGrid.var_names match DataFrame.columns types.
- 002_fix: Implement minimal change to indexing in PairGrid.map_diag / map_offdiag to use .iloc with integer index derived from column position, or to use .loc[:, var] which accepts tuple keys for MultiIndex. Prefer .loc[:, var]. Use self.data[var] currently; replace with self.data.loc[:, var]
- 003_review: Code review pass
- 004_qa: Run tests

Next
- Create the tickets and hand off to Engineer.
