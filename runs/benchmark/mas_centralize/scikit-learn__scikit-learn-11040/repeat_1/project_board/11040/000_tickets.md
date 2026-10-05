Tickets for issue #11040 - Missing parameter validation in Neighbors estimator for float n_neighbors

T1 - Triage & narrow scope
- File an analysis ticket to find where n_neighbors is accepted/used for NearestNeighbors, KNeighborsClassifier/Regressor, RadiusNeighbors, and their kneighbors/kneighbors_graph methods. Identify a minimal set of call sites to add validation.
- Owner: ProjectManager (Alice)

T2 - Implement central validation helper
- Add a helper function (e.g., _check_n_neighbors) in sklearn/neighbors/_base.py (or an appropriate shared module) that validates n_neighbors:
  - Accepts int >=1
  - Accepts float if it is integer-like (i.e., float.is_integer() == True), cast to int
  - Rejects other types with a ValueError (with message explaining expected integer)
  - Raise ValueError for non-positive values
- Add unit tests for helper if reasonable.
- Owner: Engineer

T3 - Apply validation in NearestNeighbors.fit and kneighbors
- Call the helper for n_neighbors passed via constructor and kneighbors kwargs before passing to KD-tree code. Ensure argument precedence is respected (kneighbors's n_neighbors overrides constructor's).
- Owner: Engineer

T4 - Update other estimators/entrypoints where n_neighbors is accepted
- Apply the same helper in KNeighborsClassifier, KNeighborsRegressor, neighbors_graph functions as needed (only where failing tests indicate necessity). Minimize modifications.
- Owner: Engineer

T5 - Code review
- Lightweight review to ensure change is minimal and message is clear.
- Owner: CodeReviewer

T6 - QA run
- Run affected test(s) including sklearn/neighbors/tests/test_neighbors.py::test_n_neighbors_datatype and full neighbors test suite.
- Verify QA_VERDICT verified: true before closing.
- Owner: QA

T7 - ProjectManager closeout
- Confirm non-empty patch present, QA verdict true, and produce PROJECT COMPLETE summary.
- Owner: ProjectManager (Alice)

Notes:
- The harness already applied test patch. Focus on implementation changes. Do not edit tests.
- Completion requires engineer and QA handoffs.