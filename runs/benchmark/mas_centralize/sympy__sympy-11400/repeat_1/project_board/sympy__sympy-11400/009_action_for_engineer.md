URGENT (Engineer): One-line rename and commit — blocking QA

Summary:
- Current ccode change implements sinc handling but the method is named _print_sinc (lowercase s).
- SymPy printer requires method name to match class name Sinc, so method must be _print_Sinc.

Required minimal change (apply immediately):
1. Edit sympy/printing/ccode.py and rename the method:

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

2. Commit the change with a clear message, e.g.:
   "fix(ccode): handle Sinc in CCodePrinter"

3. Ensure the commit is visible to the harness/read_patch_diff (non-empty patch.diff).

4. Run the tests (or let CI run them):
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_sinc
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_Relational

5. After test run, hand off to QA and request a QA_VERDICT block with verified: true/false and failing_ids (if any).

Notes for QA (once Engineer confirms commit):
- If QA cannot run pytest in this environment (pytest not found), notify ProjectManager and include QA_VERDICT with verified:false and failing_ids explaining the environment issue.

Failure modes and remediation:
- If tests still fail after rename, include failing test ids and stack traces; route back to Engineer to fix.

Deliverable:
- A commit containing the rename and a passing QA_VERDICT with verified: true.
