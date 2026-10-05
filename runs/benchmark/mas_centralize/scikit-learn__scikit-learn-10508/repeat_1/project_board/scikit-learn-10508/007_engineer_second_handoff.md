Engineer second handoff:

I updated the patch per the code review.

Changes:
- transform: now returns np.array([], dtype=np.intp) for empty inputs (platform-native int)
- inverse_transform: returns np.array([], dtype=self.classes_.dtype) for empty inputs to preserve original label dtype

Files changed:
- sklearn/preprocessing/label.py

Local checks: ran some quick pytest commands; full CI not run here. Please proceed to QA.
