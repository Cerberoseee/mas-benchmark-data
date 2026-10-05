Issue: LabelEncoder.transform fails for empty lists when classes are strings
Repository: scikit-learn/scikit-learn
Base commit: c753b77ac49e72ebc0fe5e3c2369fe628f975017

Summary:
LabelEncoder.transform([]) raises a TypeError when the encoder was fit
on string data. The root cause is numpy constructing an empty array of
float64 for [] which cannot be safely cast to the string dtype of
classes_ during np.searchsorted. Expected behavior: transforming an
empty list should return an empty integer array regardless of fitted dtype.

Goal:
Create small, focused changes in sklearn.preprocessing.label_.LabelEncoder
so that transform handles empty inputs robustly, and add tests covering
both numeric and string-fitted cases.

Planned tickets:
- T1: Investigate and implement fix in LabelEncoder.transform to handle
  empty inputs without dtype casting errors.
- T2: Add unit tests for empty inputs with numeric and string classes.
- T3: Code review and scope check.
- T4: QA validation (run failing tests and ensure all label tests pass).

Workflow:
Engineer implements the minimal change. CodeReviewer performs code review
(focus on correctness and surface area). QA runs tests and returns QA_VERDICT
with verified:true/false.

Notes:
- The harness already applied the failing test patch. Implementation change
  is expected here.
- Ensure final patch is non-empty and passed through review and QA before
  marking project complete.