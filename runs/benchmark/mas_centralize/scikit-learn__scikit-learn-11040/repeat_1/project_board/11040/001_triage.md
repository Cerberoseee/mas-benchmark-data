Triage notes

Files to inspect for n_neighbors handling:
- sklearn/neighbors/_base.py   (base classes for neighbors and shared helpers)
- sklearn/neighbors/_classification.py
- sklearn/neighbors/_regression.py
- sklearn/neighbors/_unsupervised.py (NearestNeighbors)
- sklearn/neighbors/_graph.py (kneighbors_graph)
- sklearn/neighbors/binary_tree.pyx / kd_tree.pyx (Cython internals) - we won't change these

Tests failing: sklearn/neighbors/tests/test_neighbors.py::test_n_neighbors_datatype
Open questions:
- Where does kneighbors accept n_neighbors kwarg? In NearestNeighbors.kneighbors implementation and in KNeighborsClassifier.kneighbors (inherited?). We'll add validation centrally in the base class (NearestNeighbors) and possibly in KNeighborsMixin if present.

Decision:
- Implement helper in sklearn/neighbors/_base.py and call it from NearestNeighbors.kneighbors and from methods that accept n_neighbors parameter.
- Favor ValueError for invalid values and accept integer-like float by casting.

Next: route to Engineer to implement T2-T4.