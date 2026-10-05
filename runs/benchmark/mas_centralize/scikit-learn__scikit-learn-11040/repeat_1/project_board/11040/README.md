Issue: Missing parameter validation in Neighbors estimator for float n_neighbors

Repo: scikit-learn/scikit-learn
Base commit: 96a02f3934952d486589dddd3f00b40d5a5ab5f2

Problem:
When passing a float like 3.0 for n_neighbors to NearestNeighbors.fit or kneighbors, a TypeError occurs deep in the Cython KD-tree implementation because a float is passed where an int is expected. We need to validate and give a clear error, and ensure kneighbors(X, n_neighbors=3.0) is also handled.

Goal:
- Validate n_neighbors is an integer-like positive scalar when accepted as a parameter (either in constructor or kneighbors call).
- Raise a helpful ValueError if a non-integer float is passed (e.g., 3.5) or a negative value, or TypeError if wrong type that can't convert.
- Allow integer-like floats (e.g., 3.0) by accepting/casting them to int.

Constraints:
- Minimize change surface; do not alter downstream KD-tree Cython code unless necessary.
- Ensure tests pass including test_n_neighbors_datatype.

Plan: Triage, implement, review, QA.
