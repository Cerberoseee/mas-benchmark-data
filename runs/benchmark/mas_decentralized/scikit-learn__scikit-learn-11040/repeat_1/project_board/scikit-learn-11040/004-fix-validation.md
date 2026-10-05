T-11040: Added validation for n_neighbors in NeighborsBase.

- Implemented TypeError for float n_neighbors during fit and kneighbors.
- Added ValueError for non-positive n_neighbors in kneighbors when provided as argument.
- Committed changes to sklearn/neighbors/base.py.

Tests:
- Ran test_n_neighbors_datatype and unsupervised_kneighbors locally; they pass.
