Title: QA validation for RidgeClassifierCV store_cv_values

Description:
Run the relevant test(s) and verify that cv_values_ are present when store_cv_values=True and cv=None. Provide QA_VERDICT block with verified:true/false and failing_ids if any.

Test commands:
- pytest -q sklearn/linear_model/tests/test_ridge.py::test_ridge_classifier_cv_store_cv_values
- Optionally run the whole test file.

QA responsibilities:
- Confirm cv_values_ shape and existence per docs.
- If failing, capture traceback and failing test ids.

Owner: QA

Priority: High
