Ticket: Apply optional Float printer refinement (uppercase 'E')

Context:
- Current committed patch adds _print_Float in sympy/printing/mathematica.py that replaces lowercase 'e' with '*^'.
- CodeReviewer suggested also handling uppercase 'E' for robustness.
- The Engineer encountered a hard-stop and cannot apply another commit in this run. This ticket requests a small, safe change to be applied by a maintainer or another engineer.

Patch to apply (unified diff):
--- a/sympy/printing/mathematica.py
+++ b/sympy/printing/mathematica.py
@@
     def _print_Float(self, expr):
-        res = str(expr)
-        return res.replace("e", "*^")
+        res = str(expr)
+        return res.replace('e', '*^').replace('E', '*^')

Why this is safe:
- Minimal single-line change; Python's str(float) normally emits lowercase 'e', so this is defensive and will not change typical output.
- Limits change surface to a single method in printing/mathematica.py.

Acceptance criteria:
- Commit the above change in sympy/printing/mathematica.py and push.
- Run the targeted QA commands once pytest is available in the harness:
  - pytest --collect-only sympy/printing/tests/test_mathematica.py::test_Derivative -q
  - pytest -q sympy/printing/tests/test_mathematica.py::test_Derivative
- Update the project board with the QA output (QA_VERDICT block). If QA returns verified: true, Project Manager will finalize.

Notes for the maintainer applying the patch:
- Do not modify tests. Only touch sympy/printing/mathematica.py.
- After committing, re-run the targeted test locally or in CI, and paste outputs to the board to help QA.
