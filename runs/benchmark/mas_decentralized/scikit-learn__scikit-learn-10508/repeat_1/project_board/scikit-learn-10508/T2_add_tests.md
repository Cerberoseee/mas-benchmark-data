Title: T2 - Add tests for LabelEncoder.transform with empty inputs

Description:
Add unit tests to ensure LabelEncoder.transform handles empty inputs for
encoders fit on numeric data and on string data. Ensure both list and
numpy array empty inputs are covered.

Tests to add:
- test_label_encoder_empty_array_numeric: fit on [1,2], transform([])
  returns empty integer array.
- test_label_encoder_empty_array_strings: fit on ["a","b"],
  transform([]) returns empty integer array.
- test_label_encoder_empty_array_numpy_with_dtype: ensure transforming
  np.array([], dtype=original_dtype) works.

Location: sklearn/preprocessing/tests/test_label.py

Estimate: small (0.5-1 hour).

Assignee: Engineer.