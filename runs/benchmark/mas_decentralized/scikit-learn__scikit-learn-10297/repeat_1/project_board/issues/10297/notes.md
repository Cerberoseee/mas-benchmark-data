Status: Fixed

I added the store_cv_values parameter to RidgeClassifierCV so it is passed to _BaseRidgeCV and exposed on the classifier. Updated behavior validated by running targeted tests.

Changed file: sklearn/linear_model/ridge.py
Tested: sklearn/linear_model/tests/test_ridge.py::test_ridge_classifier_cv_store_cv_values and related ridge tests.
