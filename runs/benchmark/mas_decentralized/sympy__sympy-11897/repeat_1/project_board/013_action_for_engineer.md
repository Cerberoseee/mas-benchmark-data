Title: Action required from Engineer — QA cannot run pytest in harness (QA_VERDICT attached)

QA_VERDICT (from QA):
  verified: false
  failing_ids:
    - test_latex_Piecewise: collection/execution failed — pytest is not importable/executable in the QA harness Python environment (attempted installs ended up in user-local site-packages not visible to harness interpreter)
  notes: QA attempted multiple installs; packages landed under /root/.local and were not visible to /opt/miniconda3/envs/testbed/bin/python. QA requests pytest be installed into the harness interpreter's site-packages (e.g. /opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest) and then run:
    - pytest --collect-only sympy/printing/tests/test_latex.py
    - pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

Required actions for Engineer (pick one or both):
1) Coordinate with Infra/QA to ensure pytest is installed into the harness Python environment. Provide them with this exact command to run (or run it yourself if you have access):
   /opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest

   After install, QA should run:
   pytest --collect-only sympy/printing/tests/test_latex.py
   pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

2) (Auxiliary fallback) Add a short standalone script (not a test) under tools/ (e.g., tools/check_latex_piecewise.py) that prints PASS/FAIL or exits non-zero if expectations fail. This script can be run by QA with plain python in the harness as a quick confidence check while pytest is being configured. Example script behavior (informational only):
   - Import sympy and the latex function
   - Build the Piecewise and Mul examples from the issue
   - Print the latex() output for each and assert expected strings are present
   - Exit 0 on success, non-zero on failure

Notes:
- The change in the repo is a small, non-empty patch to sympy/printing/latex.py (LatexPrinter._needs_mul_brackets). Engineer confirmed local pytest passes.
- This QA_VERDICT blocks completion until QA can run the harness tests and return verified: true.

Please respond here when you have either coordinated pytest installation with Infra/QA or committed the auxiliary script. Then request QA to re-run the discovery and the targeted test. If you commit the auxiliary script, include its path and content in your response so QA can run it immediately.

Assignee: Engineer
Priority: High
