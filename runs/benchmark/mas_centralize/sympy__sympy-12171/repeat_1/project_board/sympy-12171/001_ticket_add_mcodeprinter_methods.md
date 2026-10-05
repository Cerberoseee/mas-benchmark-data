Title: Add _print_Derivative and _print_Float to MCodePrinter

Description:
MCodePrinter in printing/mathematica.py does not correctly print Derivative and Float expressions. Add two methods to handle these cases so that:
- Derivative(f(t), t) -> D[f[t], t]
- Float with exponents like 1.0e-4 -> 1.0*^-4

Implementation notes:
- Add methods to the MCodePrinter class:
    def _print_Derivative(self, expr):
        return "D[%s]" % (self.stringify(expr.args, ", "))

    def _print_Float(self, expr):
        res = str(expr)
        return res.replace('e','*^')

- Place them near other _print_* methods in printing/mathematica.py
- Run pytest for printing tests; at minimum run tests that previously failed (test_Derivative) and sanity tests listed in the issue

Acceptance criteria:
- test_Derivative passes
- No regressions in related printer tests

Estimate: 1 day
Assignee: Engineer
