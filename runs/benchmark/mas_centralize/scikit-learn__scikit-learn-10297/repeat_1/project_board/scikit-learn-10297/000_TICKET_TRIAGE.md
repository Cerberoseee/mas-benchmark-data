Title: RidgeClassifierCV: add store_cv_values parameter support

Summary:
RidgeClassifierCV currently does not accept the store_cv_values init parameter, although the documentation and related code paths expect it. This causes a TypeError when users pass store_cv_values=True. A test exists that fails: sklearn/linear_model/tests/test_ridge.py::test_ridge_classifier_cv_store_cv_values.

Goal:
Add minimal support for store_cv_values to RidgeClassifierCV, ensuring the attribute cv_values_ is populated when requested and cv=None. Keep changes localized and covered by tests.

Proposed approach:
- Inspect RidgeClassifierCV __init__ signature and internal use of attributes.
- Mirror RidgeCV implementation for store_cv_values handling (it's present there).
- Add parameter store_cv_values: bool = False to RidgeClassifierCV.__init__ and store it on self.
- Ensure fit populates cv_values_ when store_cv_values True and cv is None.
- Add or use existing tests: ensure test_ridge_classifier_cv_store_cv_values passes.

Acceptance criteria:
- New/modified tests pass locally: at least test_ridge_classifier_cv_store_cv_values.
- No regressions in other ridge tests.

Assignees: Engineer -> CodeReviewer -> QA -> ProjectManager

Notes:
- Prefer minimal change; reuse RidgeCV logic where feasible.
- Tests in repo indicate similar functionality for RidgeCV exists.
- Follow repository style and patterns.
