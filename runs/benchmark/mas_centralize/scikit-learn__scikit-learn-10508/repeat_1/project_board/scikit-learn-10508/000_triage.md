Title: LabelEncoder.transform fails on empty lists for certain fitted dtypes

Repository: scikit-learn/scikit-learn
Issue: scikit-learn#10508 (SWE-bench task)

Summary:
LabelEncoder.transform([]) raises a TypeError when the encoder was fit
on string data, because numpy creates an empty float64 array from [] and
np.searchsorted attempts unsafe casting to the string dtype.

Goal:
Fix LabelEncoder.transform so that transforming empty sequences returns an
empty integer array regardless of the fitted classes_ dtype.

Scope & constraints:
- Minimal change surface: adjust transform only to handle empty inputs.
- Do not modify tests; harness already applied test patches if needed.
- Provide engineer implementation, code review, and QA validation per
  SWE-bench workflow.

Investigation notes:
- The bug occurs because np.asarray([]) yields dtype float64; when classes_
  are unicode strings, np.searchsorted calls cause a TypeError due to unsafe
  casting rules.
- Workaround: coerce the empty input to the dtype of classes_ before calling
  np.searchsorted (e.g., np.asarray(y, dtype=self.classes_.dtype)).
- Must ensure behavior for both empty and non-empty inputs remains correct.

Proposed fix:
- In LabelEncoder.transform, detect empty input early (y.size == 0) and
  return np.array([], dtype=np.intp) or maybe int64 consistent with other
  outputs. Alternatively, cast y to classes_.dtype before searchsorted.
- Prefer cast approach to preserve behavior for non-empty arrays.

Tickets:
1) 001_fix_labelencoder_empty_input: Implement changes in
   sklearn/preprocessing/label.py to ensure empty inputs are handled.
2) 002_unit_tests_check: Ensure existing tests pass locally (CI will run
   them). (No test file changes expected.)
3) 003_code_review: Request reviewer to verify patch scope and style.
4) 004_qa_validation: Run test suite target tests and report QA_VERDICT.

Assignees:
- Engineer: @maykulkarni (per user message volunteering)
- CodeReviewer: @reviewer
- QA: @qa

Next step: create engineer ticket and transfer to Engineer.
