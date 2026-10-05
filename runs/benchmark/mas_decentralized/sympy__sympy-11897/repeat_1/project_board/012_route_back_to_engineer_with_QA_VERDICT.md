Title: Action needed from Engineer — QA cannot run pytest in harness

QA_VERDICT (from last QA run):
  verified: false
  failing_ids:
    - test_latex_Piecewise: collection/execution failed — pytest is not importable/executable in the QA harness Python environment (attempted installs ended up in user-local site-packages not visible to harness interpreter)
  notes: QA attempted multiple installs; packages landed under /root/.local and were not visible to /opt/miniconda3/envs/testbed/bin/python. QA requests pytest be installed into the harness interpreter's site-packages (e.g. /opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest) and then run:
    - pytest --collect-only sympy/printing/tests/test_latex.py
    - pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

Required actions for Engineer:
1) Confirm the committed patch is final and non-empty. (It is: sympy/printing/latex.py changed.)
2) Coordinate with Infra/QA to ensure pytest is installed into the harness Python environment. Provide the exact command they should run and, if helpful, offer to run that command yourself if you have access to the harness environment. Suggested command to give to Infra:
   /opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest

3) As a fallback to help QA unblock quickly, add a small standalone verification script (not a test file) under tools/ or scripts/ in the repo that the QA harness can execute via plain python to validate the specific printing outputs (this is only an auxiliary check; per workflow QA still must run pytest eventually). Suggested script path: tools/check_latex_piecewise.py with simple assertions and clear exit codes or printed PASS/FAIL.
   - The script should not modify tests and should not be used as a replacement for pytest-driven QA_VERDICT.

4) Once pytest is available in the harness, ask QA to re-run the DISCOVERY FIRST and targeted test and report the QA_VERDICT.

Notes:
- QA tried to add /root/.local to sys.path and run pytest from that location but the harness still could not import pytest; installing pytest with the harness Python is necessary.
- The change itself is intentionally small; engineer reports the targeted test passes locally.

Please respond here when you've either coordinated pytest installation with Infra or committed the auxiliary verification script, and request QA re-run.  

Assignee: Engineer
Priority: High
