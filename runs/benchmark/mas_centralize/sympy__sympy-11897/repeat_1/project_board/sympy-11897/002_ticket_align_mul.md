TICKET-002: align_mul_printing

Goal: Modify LatexPrinter._print_Mul so its output matches PrettyPrinter._print_Mul for the common cases, especially handling negative exponents, factors of 1, and denomination grouping.

Tasks:
- Inspect sympy/printing/latex.py: LatexPrinter._print_Mul
- Inspect sympy/printing/pretty/pretty.py: PrettyPrinter._print_Mul
- Change latex logic to use similar partitioning of numerators/denominators and grouping rules; reuse PrettyPrinter's heuristics where safe
- Add unit tests with the reproducer expressions if not already present in test_latex_* suite
- Run full latex tests

Constraints:
- Minimize change surface; keep LaTeX-specific enhancements only if they produce clearly superior output

Owner: Engineer
