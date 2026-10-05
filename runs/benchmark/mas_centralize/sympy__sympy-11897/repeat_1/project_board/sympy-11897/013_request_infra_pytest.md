Request: Install pytest in test harness environment

Recommendation: Option A (request harness/infra to add pytest) — preferred.

Reasoning:
- QA could not run the targeted test due to pytest not being available in the workspace. This is an infra issue blocking verification.
- Installing pytest in the test harness allows QA to run the tests in the same controlled environment that the rest of the CI uses, ensuring a reliable verification step. Running tests locally may not replicate harness conditions.

Action requested from infra (minimal):
- Ensure the test Python environment used by the harness has pytest available.
- Installation options (pick one depending on harness setup):
  - pip install pytest (system or venv used by the harness)
  - conda install -n testbed pytest (if the harness uses conda env 'testbed')

Post-installation QA steps (to be run by QA):
- python3 -m pytest --collect-only sympy/printing/tests/test_latex.py -q
- python3 -m pytest sympy/printing/tests/test_latex.py::test_latex_Piecewise -q
- If successful, QA should return QA_VERDICT with verified: true. If failures occur, include failing_ids and stdout/stderr.

Context and references:
- Patch applied to: sympy/printing/latex.py (modified _needs_mul_brackets to bracket Piecewise and detect top-level container instances). Changes have CodeReviewer approval.
- QA could not proceed because pytest is missing. See project_board/sympy-11897/008_qa_feedback.md for QA logs.

Owner: infra to install pytest; QA to run verification after installation.

Please update this ticket when pytest is installed and QA has been notified to re-run the tests.
