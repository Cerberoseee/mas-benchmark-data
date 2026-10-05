Ticket: 001_fix_labelencoder_empty_input

Summary:
Fix LabelEncoder.transform to correctly handle empty input sequences even
when the encoder was fit on non-numeric types (e.g., strings). Transforming
an empty list/array should return an empty integer array instead of
raising a TypeError.

Files to change:
- sklearn/preprocessing/label.py

Acceptance criteria:
- The following tests must pass:
  - sklearn/preprocessing/tests/test_label.py::test_label_encoder_errors
  - sklearn/preprocessing/tests/test_label.py::test_label_encoder_empty_array
- No other tests should be negatively affected.
- The change should be minimal and local to transform method.

Implementation notes:
- Convert input y via np.asarray(y, dtype=self.classes_.dtype) before
  calling np.searchsorted, but only when y is empty or when dtype differs
  to avoid unexpected upcasting for numeric cases.
- Alternatively detect empty array early and return np.empty(0, dtype=intp)
  or np.array([], dtype=int64) to match existing outputs.

Estimate: 1-2 hours.

Assigning to: Engineer (@maykulkarni)
