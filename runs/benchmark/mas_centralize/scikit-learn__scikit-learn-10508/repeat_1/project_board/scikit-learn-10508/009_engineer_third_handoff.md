Engineer third handoff:

I adjusted the implementation per QA feedback.

Changes made:
- transform: for empty input now returns np.array([]) (default dtype) instead of np.intp
- inverse_transform: for empty input returns np.array([]) (default dtype) to match existing tests
- Kept column_or_1d call in both transform and inverse_transform for input validation

Files changed:
- sklearn/preprocessing/label.py

Local quick check: ran targeted tests; one test previously failing now passes locally per quick run. Please re-run QA test suite.
