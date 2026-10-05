Title: QA failed to run tests — route back to Engineer

QA_VERDICT (from QA run):
  verified: false
  failing_ids:
    - test_latex_Piecewise: collection/execution failed — pytest not found in environment (could not run `pytest --collect-only`)
  notes: test file exists but QA could not collect/run tests due to missing pytest. Please enable pytest in the workspace and re-run the targeted collection and tests.

Action requested from Engineer:
1) Confirm the committed patch is final and non-empty (commit 0fda42e... changed sympy/printing/latex.py). Confirm you did not edit any test files.
2) Run the following locally (or in the CI environment) to ensure collection succeeds and the test passes:
   - pytest --collect-only sympy/printing/tests/test_latex.py
   - pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise
   If pytest is not installed in your environment, install it with:
     python -m pip install -U pytest
3) If pytest collection fails (e.g., due to SyntaxError / ImportError) then fix and commit a new patch. If the only problem is the QA environment missing pytest, respond confirming that and provide the one-liner above so QA can install it and re-run.
4) When done, reply here (or push a new patch) and request CodeReviewer review again.

Notes for Engineer:
- QA could not verify anything because pytest is missing. This is an infrastructure issue; however please still run the collection and targeted tests locally to ensure your change doesn't introduce import/collection errors.
- If you want me to, I will ask CodeReviewer to re-run the tests after you confirm pytest is available or after you push a new patch.
