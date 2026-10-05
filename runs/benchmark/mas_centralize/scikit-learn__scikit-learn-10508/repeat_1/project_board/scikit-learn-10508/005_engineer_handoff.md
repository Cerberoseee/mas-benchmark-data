Engineer handoff:

I implemented a minimal patch in sklearn/preprocessing/label.py to handle
empty inputs in both transform and inverse_transform.

Patch summary:
- LabelEncoder.transform: if y.size == 0 -> return np.array([], dtype=np.int64)
- LabelEncoder.inverse_transform: early return np.array([]) for empty input

Files changed:
- sklearn/preprocessing/label.py

Local tests run by Engineer (selected):
- pytest sklearn/preprocessing/tests/test_label.py -> some tests passed, three xfail/skip marked with x in output

Please pick this up for code review.
