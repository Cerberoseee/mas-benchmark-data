Tickets for issue 10297

TICKET-1: Add store_cv_values parameter to RidgeClassifierCV
- Modify sklearn/linear_model/ridge.py to add store_cv_values to RidgeClassifierCV.__init__ signature with default False.
- Ensure attribute self.store_cv_values exists.
- Use minimal changes, mirroring RidgeCV implementation.
- Add logic so that when store_cv_values is True and cv is None, cv_values_ is computed/stored during fit.
- Add necessary imports or utility usage as in RidgeCV.

TICKET-2: Implement cv_values_ computation in fit
- Ensure that during cross-validation when cv=None and store_cv_values is True, the classifier records cv_values_ with shape matching documentation.
- Reuse code paths from RidgeCV where possible.

TICKET-3: Add/enable test
- Ensure sklearn/linear_model/tests/test_ridge.py::test_ridge_classifier_cv_store_cv_values exists and passes.
- Update or add small unit test if missing or adjusted behavior.

TICKET-4: Run test subset and validate
- Run the failing test and related Ridge tests locally or via CI.
- Capture failures; iterate if necessary.

TICKET-5: Code review handoff
- Create PR and request CodeReviewer review. Include brief description and reference to failing test.

TICKET-6: QA handoff
- Once CodeReviewer approves, hand to QA for final verification and to produce QA_VERDICT.

Notes
- Keep changes minimal and backward compatible.
- Do not change public API beyond adding optional parameter.
