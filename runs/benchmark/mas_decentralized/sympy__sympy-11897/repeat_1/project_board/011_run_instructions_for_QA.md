Run instructions for QA (install pytest and verify test)

Purpose:
QA should install pytest into the harness/test-runner Python environment and run the DISCOVERY FIRST collection and the targeted test for test_latex_Piecewise.

1) Install pytest into the exact Python interpreter used by the test harness. Use this command (adjust the python path if your harness uses a different interpreter):

/opt/miniconda3/envs/testbed/bin/python -m pip install -U pytest

2) Verify pytest is importable/executable by that interpreter:

/opt/miniconda3/envs/testbed/bin/python -m pytest --version
# or
/opt/miniconda3/envs/testbed/bin/python -c "import pytest; print(pytest.__version__)"

3) Run DISCOVERY FIRST and then the targeted test (either plain pytest or the python -m form; use whichever is compatible with your harness):

pytest --collect-only sympy/printing/tests/test_latex.py
pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

# If you must invoke python explicitly:
/opt/miniconda3/envs/testbed/bin/python -m pytest --collect-only sympy/printing/tests/test_latex.py
/opt/miniconda3/envs/testbed/bin/python -m pytest -q sympy/printing/tests/test_latex.py::test_latex_Piecewise

4) Report the results here and include a QA_VERDICT block with the following fields:

QA_VERDICT:
  verified: true|false
  failing_ids:
    - <test_id>: <reason/traceback if any>
  notes: <diagnostics / environment notes>

Notes / troubleshooting:
- If previous pip installs created user-local scripts (e.g., /root/.local/bin/pytest) but the harness Python cannot import pytest, that means the pip install didn't target the harness interpreter. Use the harness interpreter with python -m pip install ... to install into the correct site-packages.
- If you cannot install into the harness interpreter due to policy, report that here. As an interim manual check (not a substitute for the required pytest run), you can run the quick python script below to print the specific latex outputs for sanity checking.

Optional quick sanity-check (auxiliary only):

/opt/miniconda3/envs/testbed/bin/python - <<'PY'
from sympy import symbols, exp, log, Piecewise, latex
A = symbols('A')
x, mu, sigma = symbols('x mu sigma')
p = Piecewise((x, x < 1), (x**2, True))
print("Piecewise latex:", latex(p))
print("A * Piecewise latex:", latex(A*p))
print("exp(-(x-mu)**2/sigma**2) latex:", latex(exp(-(x - mu)**2/sigma**2)))
print("exp(-x)*log(x) latex:", latex(exp(-x)*log(x)))
PY

Reminder for QA: per the workflow you MUST run DISCOVERY FIRST with pytest --collect-only before executing tests and you MUST include a QA_VERDICT block in your result message. If QA_VERDICT: verified: true, the Project Manager will declare PROJECT COMPLETE after confirming the patch is non-empty (it is).