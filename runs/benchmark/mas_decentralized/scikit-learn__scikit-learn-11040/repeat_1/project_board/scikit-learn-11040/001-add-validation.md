Title: 001-add-validation: Validate n_neighbors type in NearestNeighbors

Description:
Add a small validation helper and use it to validate n_neighbors in NearestNeighbors initialization and kneighbors method so that passing a float (e.g., 3.0) raises a clear ValueError instead of a TypeError deep in Cython.

Acceptance criteria:
- Passing a float for n_neighbors in the constructor raises ValueError with a helpful message.
- Passing a float for n_neighbors to kneighbors also raises ValueError.
- Existing neighbors tests continue to pass except for the previously failing test which should now pass.

Implementation notes:
- Implement helper _validate_n_neighbors(value, name='n_neighbors') in sklearn/neighbors/_base.py.
- Use numbers.Integral to allow Python ints and numpy integer types.
- Raise ValueError("n_neighbors must be an integer, got %r" % value) for floats.
- Add calls in NearestNeighbors.__init__ and in the kneighbors method where n_neighbors is accepted as a parameter.

Files to modify:
- sklearn/neighbors/_base.py

Estimated effort: small
