QA handback -> Engineer action required

QA_VERDICT:
  verified: false
  failing_ids:
    - test_ccode_sinc: implementation incomplete — CCodePrinter defines def _print_sinc(...) (lowercase) so the Sinc handler will not be dispatched; must be renamed to _print_Sinc and committed.
    - test_ccode_Relational: not validated in this environment — pytest not available here so tests could not be executed to confirm pass; although _print_Relational is present, please run the test in CI after the above rename.
  notes: Found sinc handler implemented but misnamed (_print_sinc); pytest is not available in this environment so QA could not run tests. Rename to _print_Sinc, commit, and run the two tests in CI — then provide an updated QA_VERDICT.

Engineer tasks (explicit):
1) Edit sympy/printing/ccode.py and rename the method:
   def _print_sinc(self, expr):
   ->
   def _print_Sinc(self, expr):
   (Do not change the body; only rename.)
2) Commit the change with an informative message, e.g. "fix(ccode): handle Sinc in CCodePrinter".
3) Ensure the commit is visible to the harness (read_patch_diff should show a non-empty patch.diff).
4) Run the two tests locally if possible, or rely on CI/harness to run them:
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_sinc
   - pytest -q sympy/printing/tests/test_ccode.py::test_ccode_Relational
5) If tests pass, push changes and notify QA. Provide updated QA_VERDICT with verified: true.
6) If tests fail, include failing_ids and full trace; route back to QA after fixing.

Constraints:
- Minimal surface: only touch sympy/printing/ccode.py.
- Do not modify tests.

Deliverable:
- A commit renaming the method and a passing QA_VERDICT.
