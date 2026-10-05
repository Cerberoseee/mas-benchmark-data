Title: QA: Validate MCodePrinter changes

Description:
Run targeted tests for the Mathematica code printer after the engineer's patch is applied.

Tasks:
- Run pytest --collect-only sympy/printing/tests/test_mathematica.py -q and confirm test IDs include test_Derivative
- Run pytest -q sympy/printing/tests/test_mathematica.py::test_Derivative
- Optionally run the full sympy/printing/tests/test_mathematica.py test module

Acceptance criteria:
- QA verifies that test_Derivative passes
- QA reports QA_VERDICT block with verified: true/false and failing_ids if false

Notes:
- The environment in the harness may not have pytest installed. If pytest is missing, please report that in the QA_VERDICT and mark verified: false.

Assignee: QA
