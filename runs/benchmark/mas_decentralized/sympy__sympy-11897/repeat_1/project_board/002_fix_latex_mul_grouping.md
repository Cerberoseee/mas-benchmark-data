Title: Fix LaTeX Mul grouping to match pretty printer

Description:
Implement minimal changes in sympy/printing/latex.py (LatexPrinter._print_Mul) to produce output consistent with PrettyPrinter._print_Mul for cases like:
- exp(-x)*log(x) -> prefer e^{-x} \log(x) over \frac{1}{e^{x}} \log(x)
- 1/(x+y)/2 -> prefer the pretty printer grouping with explicit numerator/denominator grouping: numerator 1 over (2*(x+y)) rather than 1/(2x+2y)

Requirements:
- Keep LaTeX-specific enhancements where they provide strictly better output.
- Add unit tests only if necessary; prefer passing existing tests.

Assignee: Engineer
Priority: High

Acceptance criteria:
- Implemented patch committed.
- Non-empty patch recorded in project board.
- Request code review after implementation.
