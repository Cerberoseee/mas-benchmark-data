QA feedback (from QA run):

QA_VERDICT:
  verified: false
  failing_ids:
    - test_latex_Piecewise: pytest collection failed (pytest not installed in environment; could not collect/run the test)
  notes: Implementation patch present and reviewed; test exists. Cannot execute pytest to validate due to missing pytest in the workspace — please ensure pytest is available in the test environment and re-run the targeted test collection/execution.

Action required by Engineer:
- Re-run the targeted tests (test_latex_Piecewise) in an environment where pytest is available.
- If the harness is missing pytest, run pytest locally or in CI and report results back to QA.
- Confirm no further code changes are needed. If changes are needed, make minimal fixes and commit a new patch.

Reference:
- Patch in sympy/printing/latex.py modifies _needs_mul_brackets to restore nested Piecewise detection and add isinstance checks for container instances.
- CodeReviewer approved the revised patch.
