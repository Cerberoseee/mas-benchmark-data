Title: Code review for RidgeClassifierCV store_cv_values change

Description:
Review the patch implementing store_cv_values for RidgeClassifierCV for correctness, style, and minimal surface area. Pay attention to API compatibility, tests, and whether cv_values_ is computed in the expected shape.

Checklist:
- __init__ signature updated and documented.
- fit method collects cv_values_ only when requested and when cv is None.
- No import cycles introduced.
- Tests updated/added pass.

Owner: CodeReviewer

Priority: Medium
