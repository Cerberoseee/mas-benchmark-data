Urgent: Rename sinc printer method and commit

Owner: Engineer

Problem:
- Current implementation in sympy/printing/ccode.py defines _print_sinc (lowercase). SymPy's printer dispatch uses the class name (Sinc), so the method must be named _print_Sinc (capital S) to be invoked.

Required changes (minimal):
1. In sympy/printing/ccode.py, rename the method

    def _print_sinc(self, expr):
        from sympy import Piecewise, sin, Ne, S
        x = expr.args[0]
        _piecewise = Piecewise((sin(x)/x, Ne(x, 0)), (S.One, True))
        return self._print(_piecewise)

   to

    def _print_Sinc(self, expr):
        from sympy import Piecewise, sin, Ne, S
        x = expr.args[0]
        _piecewise = Piecewise((sin(x)/x, Ne(x, 0)), (S.One, True))
        return self._print(_piecewise)

2. Leave other changes as-is. Do not modify tests.
3. Run pytest for the two failing tests (if environment supports it):
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_sinc
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_Relational

4. Commit the change and ensure patch.diff contains the modification (use read_patch_diff to confirm).

Notes:
- If pytest is unavailable in this environment, commit the change and the QA step in the harness will run tests. Ensure your commit is atomic and only touches ccode.py.
- After committing, return here so CodeReviewer and QA can proceed.
