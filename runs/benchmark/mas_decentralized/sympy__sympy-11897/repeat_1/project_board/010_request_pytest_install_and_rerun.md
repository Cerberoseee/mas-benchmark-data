Title: Request: install pytest in QA workspace and re-run latex printing tests

Problem:
QA cannot run pytest in the workspace: importing or executing pytest from the environment's Python fails (module not found or execution wrappers disallowed). QA attempted various installs but the pytest package was not visible to the Python interpreter used to run tests (/opt/miniconda3/envs/testbed/bin/python).

Action requested (Infra / QA):
1) Install pytest into the environment's Python site-packages using the Python executable that runs tests. Run as an allowed command:
   /opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest
   (Adjust the python path if the test environment uses a different interpreter.)

2) Ensure pytest is runnable either via pytest on PATH or via python -m pytest using the same interpreter. Verify with:
   /opt/miniconda3/envs/testbed/bin/python -m pytest --version

3) Re-run the QA collection + targeted test:
   pytest --collect-only sympy/printing/tests/test_latex.py
   pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

4) Provide QA_VERDICT block in the result message with:
   verified: true/false
   failing_ids: (list any failing test ids)
   notes: (any diagnostics, e.g., traceback or environment notes)

Context for QA:
- Engineer committed a minimal patch modifying sympy/printing/latex.py to parenthesize Piecewise in Mul (commit f4622ae7...). The patch is non-empty and only touches implementation.
- Engineer ran local pytest collection and the single test and reports it passed locally.

Acceptance criteria for this ticket:
- QA provides QA_VERDICT: verified: true AND confirms the engineer's patch is non-empty (board has the patch.diff recorded). If verified: false, QA must list failing_ids and notes so Engineer can iterate.

Assignee: QA/Infra
Priority: High
