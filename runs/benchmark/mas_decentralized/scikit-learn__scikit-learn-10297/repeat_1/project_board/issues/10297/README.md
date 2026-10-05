Issue: linear_model.RidgeClassifierCV's Parameter store_cv_values issue

Summary

RidgeClassifierCV lacks the store_cv_values boolean parameter, although the documentation and some attributes reference it (cv_values_). Passing the parameter currently raises a TypeError. A failing test exists:

- sklearn/linear_model/tests/test_ridge.py::test_ridge_classifier_cv_store_cv_values

Goal

Add store_cv_values support to RidgeClassifierCV with minimal change surface and add/update tests to validate behavior.

Investigation Plan

- Inspect RidgeClassifierCV implementation and RidgeCV (for Ridge regression) for parity.
- Add store_cv_values argument to RidgeClassifierCV.__init__ and ensure it's propagated and used consistently.
- Update internal logic to compute cv_values_ when requested and cv=None.
- Add/adjust tests: ensure test_ridge_classifier_cv_store_cv_values passes.

Workflow

Engineer: implement minimal change and ensure tests pass locally.
CodeReviewer: review diff for correctness and scope.
QA: run failing tests and provide QA_VERDICT.

Files of interest

- sklearn/linear_model/ridge.py
- sklearn/linear_model/tests/test_ridge.py

Notes

Follow existing patterns used in RidgeCV to maintain consistency.
