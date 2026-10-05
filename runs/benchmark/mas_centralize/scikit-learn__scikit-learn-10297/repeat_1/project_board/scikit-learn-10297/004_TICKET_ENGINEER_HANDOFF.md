Status: Implemented store_cv_values support in RidgeClassifierCV.

Changes: Modified sklearn/linear_model/ridge.py to add store_cv_values parameter to RidgeClassifierCV __init__ and pass it to _BaseRidgeCV. Added assignment of self.store_cv_values.

Validation: Ran targeted unit test test_ridge_classifier_cv_store_cv_values and it passed. Also ran the listed pass-to-pass ridge tests; all passed locally.

Next: Please review and run full test suite as needed.
