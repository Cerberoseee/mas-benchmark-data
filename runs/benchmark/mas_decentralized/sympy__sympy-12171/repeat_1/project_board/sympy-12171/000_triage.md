Title: Triage - Mathematica code printer: floats and Derivative not formatted correctly

Issue: The Mathematica code printer in sympy/printing/mathematica.py does not properly print Derivative objects and floats with exponents. Examples:
- Derivative(f(t), t) currently prints as Derivative(f(t), t) instead of Mathematica's D[f[t], t]
- Floats with exponents like 1.0e-4 are not converted to Mathematica's scientific notation 1.0*^-4

Failing tests:
- test_Derivative (reported failing)

Passing tests (smoke):
- test_Integer
- test_Rational
- test_Function
- test_Pow
- test_Mul
- test_constants
- test_containers
- test_Integral

Root cause hypothesis:
- MCodePrinter lacks handlers for Derivative and Float types. Adding small _print_Derivative and _print_Float methods should fix formatting.

Acceptance criteria:
- test_Derivative passes.
- All listed pass-to-pass tests continue to pass.
- Patch is minimal and only touches printing/mathematica.py (no tests edited).

Notes/Constraints:
- Tests are auto-applied by harness; do not modify tests.
- Prefer minimal, direct fix inside MCodePrinter.
- Follow normal workflow: Engineer implements -> CodeReviewer reviews -> QA validates.
