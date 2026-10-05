Ticket 008: Rename _print_sinc to _print_Sinc and commit (blocking)

Owner: Engineer (required)

Problem:
- Current implementation in sympy/printing/ccode.py defines the sinc handler as _print_sinc (lowercase s). SymPy's printer dispatch requires the method name to match the SymPy class (Sinc) so the method must be named _print_Sinc.

Required change (one-line rename):
- Edit sympy/printing/ccode.py and replace the method definition:

    def _print_sinc(self, expr):
        from sympy import Piecewise, sin, Ne, S
        x = expr.args[0]
        _piecewise = Piecewise((sin(x)/x, Ne(x, 0)), (S.One, True))
        return self._print(_piecewise)

  with:

    def _print_Sinc(self, expr):
        from sympy import Piecewise, sin, Ne, S
        x = expr.args[0]
        _piecewise = Piecewise((sin(x)/x, Ne(x, 0)), (S.One, True))
        return self._print(_piecewise)

Constraints:
- Keep the change minimal and only in ccode.py.
- Do not change tests.
- Commit the change with a clear commit message (e.g. "fix(ccode): handle Sinc in CCodePrinter").

Validation steps (post-commit):
1. Ensure read_patch_diff shows a non-empty patch diff including this rename.
2. Run tests (or let CI/harness run them):
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_sinc
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_Relational
3. After tests, route to QA and ensure QA returns QA_VERDICT block with verified:true.

Deliverable:
- Commit that renames the method and passes the two previously failing tests.
