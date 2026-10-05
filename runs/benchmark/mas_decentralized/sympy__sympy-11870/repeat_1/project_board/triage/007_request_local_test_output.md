Request for Engineer: provide local/CI test outputs so QA can verify

Background:
- Engineer committed a patch modifying Sinc._eval_rewrite_as_sin to return
  Piecewise((sin(arg)/arg, Ne(arg, 0)), (S.One, True)).
- QA cannot run pytest in the verification environment (pytest not installed), so
  QA returned verified: false. To proceed we need the Engineer to run the tests
  locally (or in CI) and paste the outputs here.

Required actions (Engineer):
1) From the repository root, in an environment with pytest installed, run and
   paste the exact outputs (stdout and pytest summary) of these commands:

   - pytest --collect-only -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc
   - pytest -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc

   Include both commands' outputs in full. If either command errors, include the
   full traceback / error output.

2) Additionally, please paste a short Python REPL transcript showing the
   rewrite behavior you intended (examples):

   - python -c "import sympy as S; k = S.symbols('k', real=True); f = S.Rational(1,2)*(-S.I*S.exp(S.I*k) + S.I*S.exp(-S.I*k)); print(f.rewrite(S.sin).simplify())"

   - For the sinc/integral example:
     python -c "import sympy as S; omega, k = S.symbols('omega k', real=True); f = S.Rational(1,2)/S.pi * S.exp(S.I*omega*k); F = S.integrate(f, (omega, -S.pi, S.pi)); print('F =', F); print('rewrite sinc:', F.rewrite(S.sinc).simplify())"

3) If tests fail locally, iterate on the patch, re-commit, and repeat steps 1-2.

Notes:
- The project manager will confirm the patch diff is non-empty via read_patch_diff
  before declaring PROJECT COMPLETE after QA verifies true.
- Do not modify tests. Focus changes only on the implementation code.

Deadline: please provide outputs here in this ticket so QA can re-run verification.
