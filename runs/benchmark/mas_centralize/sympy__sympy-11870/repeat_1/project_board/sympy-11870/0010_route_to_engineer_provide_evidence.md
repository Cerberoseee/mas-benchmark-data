Title: Action for Engineer — Provide QA evidence for test_sinc

Context:
- QA attempted to collect/run the failing test but pytest is not available in the harness. QA re-ran the collection and confirmed the environment still lacks pytest.

Latest QA_VERDICT (from QA):
  verified: false
  failing_ids:
    - test_sinc: not collected — pytest not available; collection failed with "No module named pytest"
  notes: QA cannot run pytest in the harness. They require test output or equivalent evidence that the change causes the expected behavior (sin(k) and sinc(k) rewrites).

Required from Engineer (choose one):
1) Run pytest locally or in CI with pytest installed and paste the output showing test_sinc passing.
   - Suggested command:
       pytest -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc
   - Paste full stdout/stderr logs into this ticket.

2) If pytest cannot be used, run the following Python snippet in an environment where the modified sympy package can be imported (ensure PYTHONPATH points to the repo root) and paste the exact stdout/stderr:

   python - <<'PY'
   import sys
   sys.path.insert(0, '/testbed')  # adjust if working directory differs
   from sympy import symbols, I, exp, S, sinc
   k = symbols('k', real=True)

   f = S(1)/2 * (-I*exp(I*k) + I*exp(-I*k))
   print('f =', f)
   print('f.rewrite("sin") =', f.rewrite('sin'))
   print('f.rewrite("sin").simplify() =', f.rewrite('sin').simplify())

   f2 = S(1)/2 / k * (-I*exp(I*k) + I*exp(-I*k))
   print('f2 =', f2)
   try:
       print('f2.rewrite(sinc) =', f2.rewrite(sinc))
   except Exception as e:
       print('rewrite(sinc) raised:', repr(e))
   PY

   Expected outputs:
   - first expression simplifies to sin(k)
   - second expression rewrites to an expression containing sinc(k) (or sinc(k) itself)

3) If you run pytest elsewhere (CI), paste CI logs showing test_sinc passing.

Additional checks to include with the submitted logs:
- Confirm the commit hash or diff headers for the patch (so QA can correlate the evidence with the exact code change).
- Confirm that only implementation files were modified (sympy/core/basic.py) and no test files were changed.

Deadline: please provide evidence within 24 hours to unblock QA. If you cannot run tests, explain constraints and propose an alternative plan (e.g., provide a remote CI link).

Owner: Engineer
