Ping to infra / test-harness owner:

Please install pytest in the harness test environment used for verifying sympy changes. QA attempted to run the targeted test but could not collect because pytest is missing.

Minimal options:
- pip install pytest
- or conda install -n testbed pytest

Once installed, please reply here and QA will re-run the following commands:
- python3 -m pytest --collect-only sympy/printing/tests/test_latex.py -q
- python3 -m pytest sympy/printing/tests/test_latex.py::test_latex_Piecewise -q

Context: code change already committed and code-reviewed (sympy/printing/latex.py). QA verification is blocked only by pytest availability.
