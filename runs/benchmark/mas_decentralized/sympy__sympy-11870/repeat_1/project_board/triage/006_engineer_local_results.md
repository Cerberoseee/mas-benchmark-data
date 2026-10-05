Engineer local test results and notes:

- Implemented change to sympy/functions/elementary/trigonometric.py to return Piecewise for Sinc._eval_rewrite_as_sin so rewrite('sin') yields sin(x)/x for x!=0 and 1 at x=0.
- Committed patch; patch diff verified non-empty.
- Could not run pytest within harness (pytest not installed); local validation instructions provided below.

Local validation steps for Engineer (to be run outside harness):
1. Create a virtualenv with pytest installed:
   python3 -m venv venv
   source venv/bin/activate
   pip install -e .[test]
   pip install pytest
2. Run the collection and test:
   pytest --collect-only -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc
   pytest -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc
3. Paste the output here for QA.

Notes:
- If tests pass locally, provide the pytest output as evidence so QA can accept.
- If tests fail locally, iterate on the patch and re-commit.
