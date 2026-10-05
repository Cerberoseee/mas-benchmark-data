Title: Implement store_cv_values param in RidgeClassifierCV

Description:
Add the store_cv_values boolean parameter to sklearn.linear_model.RidgeClassifierCV.__init__, store it on the estimator, and ensure fit populates cv_values_ when store_cv_values=True and cv=None.

Tasks:
- Update RidgeClassifierCV.__init__ signature to accept store_cv_values (default False).
- Assign self.store_cv_values = store_cv_values.
- In fit, when cv is None and store_cv_values True, collect cv values in the same format as RidgeCV: cv_values_ array shape [n_samples, n_alphas] or [n_samples, n_responses, n_alphas].
- Add necessary imports or helper usage (reuse code from RidgeCV if helpful).
- Run tests: focus on test_ridge_classifier_cv_store_cv_values.

Files likely to change:
- sklearn/linear_model/ridge.py (RidgeClassifierCV class)
- Possibly tests if adaptations needed (but test exists already)

Estimate: small change; ~1-2 files.

Owner: Engineer

Priority: High (fix failing test)
