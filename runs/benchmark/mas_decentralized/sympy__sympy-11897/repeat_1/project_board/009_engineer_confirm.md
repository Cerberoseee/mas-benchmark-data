Engineer confirmation

Engineer has run pytest collection locally (after installing pytest) and reports:
- pytest --collect-only sympy/printing/tests/test_latex.py collected 107 tests
- Ran pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise and it passed locally.

Engineer commit:
- New commit message: fix(latex): always parenthesize Piecewise in Mul to ensure correct grouping
- Files changed: sympy/printing/latex.py

Engineer notes:
- The patch only changes the logic in _needs_mul_brackets to remove the "not last" exception so Piecewise (and Integral/Product/Sum) are always considered to need brackets inside Mul.
- No test files were modified.

Next: request CodeReviewer to review and then transfer to QA for validation in the harness environment.
