Title: Investigate Mul printing differences between PrettyPrinter and LaTeXPrinter

Description:
Compare PrettyPrinter._print_Mul (sympy/printing/pretty/pretty.py) with LatexPrinter._print_Mul (sympy/printing/latex.py). Identify exact code paths that lead to differences in outputs for expressions like:
- exp(-x)*log(x)
- 1/(x + y)/2
- exp(-(x - mu)**2/sigma**2)
- FiniteSet(6**(S(1)/3)*x**(S(1)/3)*Piecewise(...))

Deliverables:
- A short list of code fragments in latex._print_Mul that differ from pretty._print_Mul and explanation how they affect sign handling, negative exponents, rational multipliers and denominator grouping.
- Suggested minimal code changes to latex._print_Mul to make LaTeX output consistent with pretty printer for the provided examples.

Assignee: Engineer
Priority: High

Acceptance criteria:
- A document with concrete code references and a plan for minimal change.
