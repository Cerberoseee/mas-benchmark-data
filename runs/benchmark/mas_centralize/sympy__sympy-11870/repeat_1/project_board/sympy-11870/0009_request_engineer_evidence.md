Title: Request to Engineer — provide test evidence for QA (pytest not available in harness)

Context:
- QA attempted to run the failing test (test_sinc) but the harness environment is missing pytest, so QA could not collect/run the test.
- QA_VERDICT: verified: false
  failing_ids:
    - test_sinc: not collected — pytest not available; collection failed with "No module named pytest"

Required from Engineer (pick one of the options below):
1) Run pytest locally (or in CI) against the test file and paste the output showing test_sinc passes. Commands:
   - pytest --maxfail=1 -q sympy/functions/elementary/tests/test_trigonometric.py::test_sinc
   - or pytest -q sympy/functions/elementary/tests/test_trigonometric.py

2) If pytest is not available, run a short Python snippet that imports the modified sympy package from this workspace and demonstrates the expected transformations. Example snippet to run from repository root (ensure PYTHONPATH includes the repo):

   python - <<'PY'
   import sys
   sys.path.insert(0, 'path/to/repo')  # adjust if needed
   from sympy import symbols, I, exp, S, sinc
   k = symbols('k', real=True)
   f = S(1) / 2 * (-I*exp(I*k) + I*exp(-I*k))
   print('f ->', f)
   print('f.rewrite(sin) ->', f.rewrite('sin'))
   print('f.rewrite(''sin'').simplify() ->', f.rewrite('sin').simplify())

   f2 = S(1) / 2 / k * (-I*exp(I*k) + I*exp(-I*k))
   print('f2 ->', f2)
   print('f2.rewrite(sinc) ->', f2.rewrite(sinc))
   PY

   The output should show sin(k) for the first expression and sinc(k) (or an expression containing sinc(k)) for the second.

3) If neither is possible, provide CI/test run logs showing the test passing.

Deliverable:
- Paste command output or logs into project board ticket 0009.
- Ensure read_patch_diff shows the committed patch (PM will verify). 

Owner: Engineer
Estimate: 1-2h
