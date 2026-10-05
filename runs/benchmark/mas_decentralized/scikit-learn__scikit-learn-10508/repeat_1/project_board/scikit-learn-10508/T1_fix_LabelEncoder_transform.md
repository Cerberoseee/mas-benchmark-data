Title: T1 - Fix LabelEncoder.transform to handle empty inputs

Description:
When LabelEncoder is fit on string data, calling transform([]) raises a
TypeError because numpy constructs an empty float64 array for [] which
cannot be safely cast to the string dtype of classes_. We need to make
transform handle empty inputs by returning an empty integer array of the
appropriate dtype without attempting unsafe casts.

Acceptance criteria:
- transform([]) returns array([], dtype=intp) (or dtype=int64) for
  encoders fit on numeric or string data.
- No new failures in existing label tests.
- Minimal change surface; avoid broad refactors.

Implementation notes:
- Detect empty input early (e.g., if y.size == 0) and return
  np.empty_like(y, dtype=np.intp) or np.array([], dtype=np.intp).
- Be mindful of input that is a list vs numpy array; convert to numpy
  array with correct dtype only if needed.
- Add tests in T2 for coverage.

Estimate: small (1-2 hours).

Assignee: Engineer (self-assign to implement the patch).

---

Status: Done

Notes:
- Implemented early-return for empty input in both LabelEncoder.transform
  and LabelEncoder.inverse_transform in sklearn/preprocessing/label.py.
- Commit: 272c96f8f073ea657cb28e05c693e9afd42dc411 (FIX: LabelEncoder: handle empty input in transform and inverse_transform)
- Verified with pytest: sklearn/preprocessing/tests/test_label.py passes locally (all tests in file).

Handing off to CodeReviewer and QA for review and validation.
