QA -> Engineer handoff

QA_VERDICT from latest run:
  verified: false
  failing_ids:
    - test_latex_Piecewise: pytest collection failed (pytest not installed in environment; cannot collect/run the test)
  notes: QA could not run pytest in the workspace; this is an infrastructure issue, not a code failure. The implementation patch is present and has CodeReviewer approval. QA needs pytest available to run the targeted test(s).

Required actions for Engineer:
1. Ensure the test environment can run pytest. Options:
   - If you run tests locally: install pytest in your Python environment (pip install pytest) and run the commands below.
   - If this harness should provide pytest, coordinate with infra to add pytest; else run tests locally and report results.
2. Run discovery and targeted tests:
   - python3 -m pytest --collect-only sympy/printing/tests/test_latex.py -q
   - python3 -m pytest sympy/printing/tests/test_latex.py::test_latex_Piecewise -q
   - Optionally run the latex tests subset or full test_latex.py to check for regressions.
3. Capture outputs and, if the test passes, notify QA to re-run verification. If failures occur, produce a new minimal patch and commit.

Files changed in patch:
- sympy/printing/latex.py (modified _needs_mul_brackets to bracket Piecewise and detect top-level container instances)

Context:
- CodeReviewer approved the revised patch and left no blocking findings.
- QA cannot proceed due to missing pytest.

Please re-run tests and report back with pytest outputs so QA can validate.
