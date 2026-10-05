Title: Validate n_neighbors parameter type in NearestNeighbors

Issue: Passing a float to n_neighbors (e.g., n_neighbors=3.) causes a TypeError deep in Cython kd-tree code: "'float' object cannot be interpreted as an integer". The error should be raised earlier with a helpful message (or optionally accept floats by casting). Also ensure kneighbors(..., n_neighbors=3.) raises the same helpful message.

Goal: Add validation for n_neighbors where provided (in estimator init and kneighbors call) to raise a ValueError when n_neighbors is not an integer or an integer-like value. Keep changes minimal and localized to neighbors classes. Ensure tests pass, particularly test_n_neighbors_datatype.

Files of interest:
- sklearn/neighbors/_base.py  (likely location for input validation)
- sklearn/neighbors/kde_tree.py / binary_tree.*.pxi (kd-tree backend) - avoid changing Cython; prefer Python-level checks
- sklearn/neighbors/tests/test_neighbors.py (contains failing test)

Proposed approach:
1. Add validation helper for n_neighbors in sklearn/neighbors/_base.py. Accept ints, and values that are integer-like (e.g., numpy integer dtypes). Reject floats. Use operator like isinstance(n_neighbors, numbers.Integral) or np.integer. For user-friendliness, accept values like 3.0? The failing test expects float to be rejected, so raise ValueError for floats, even if they are whole valued.
2. Validate in NearestNeighbors.__init__ for persistent parameter and inside kneighbors() for overridden call.
3. Run tests and iterate.

Tickets:
- 001-add-validation: Implement validation helper and call sites
- 002-review: Code review pass
- 003-qa: Run targeted tests

Assignees: Engineer: unassigned, Reviewer: unassigned, QA: unassigned

Notes:
- Minimize change surface; do not alter Cython code.
- The harness already applies the gold test patch. Implementation changes are expected rather than editing tests.
