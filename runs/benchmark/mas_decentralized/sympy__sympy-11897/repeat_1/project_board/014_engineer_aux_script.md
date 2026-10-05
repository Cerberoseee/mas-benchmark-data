Engineer auxiliary script for QA (optional fallback)

Path: tools/check_latex_piecewise.py

Purpose: Provide a quick standalone check QA can run with plain python if installing pytest into the harness interpreter is taking time. This script is NOT a replacement for running pytest; it simply prints the relevant latex outputs and exits with status 0 for success or 1 for failure.

Content:

#!/usr/bin/env python3
from sympy import symbols, exp, log, Piecewise, latex

A = symbols('A')
x, mu, sigma = symbols('x mu sigma')

p = Piecewise((x, x < 1), (x**2, True))
expected_p = "\\begin{cases} x & \\text{for}\\: x < 1 \\\\x^{2} & \\text{otherwise} \\end{cases}"

out_p = latex(p)
out_Ap = latex(A*p)
out_exp = latex(exp(-(x - mu)**2/sigma**2))
out_exp_log = latex(exp(-x)*log(x))

print('Piecewise latex:', out_p)
print('A * Piecewise latex:', out_Ap)
print('exp(-(x-mu)**2/sigma**2) latex:', out_exp)
print('exp(-x)*log(x) latex:', out_exp_log)

# Basic assertion (best-effort) to help QA:
if 'cases' in out_p and out_Ap.startswith('A \left('):
    print('CHECK PASSED')
    exit(0)
else:
    print('CHECK FAILED')
    exit(1)
