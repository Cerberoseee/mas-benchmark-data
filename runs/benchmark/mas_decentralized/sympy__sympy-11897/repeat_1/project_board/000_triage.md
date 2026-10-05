Title: LaTeX printer inconsistent with pretty printer

Background:
The LaTeX printer sometimes produces different formatting than the pretty (Unicode) printer for the same SymPy expression. Examples include: exp(-x)*log(x) printing as 1/e^{x} \log(x) in LaTeX but as e^{-x} ⋅ log(x) when pretty-printed (different placement of exponent). Other cases include 1/(x+y)/2 and Piecewise printing where parentheses or grouping differ.

Goal:
Make the LaTeX printer produce output consistent with the pretty printer's structural grouping where appropriate (i.e., same multiplication and division grouping), unless LaTeX can present a strictly better representation. Minimize changes and avoid broad redesign of printing subsystem.

Files/areas to inspect:
- sympy/printing/latex.py: LatexPrinter._print_Mul
- sympy/printing/pretty/pretty.py: PrettyPrinter._print_Mul

Approach:
1. Reproduce failing tests and examples locally (harness has failing test: test_latex_Piecewise).
2. Compare _print_Mul implementations in latex.py and pretty.py to find behavioral differences in how negative exponents and division are turned into 1/e^{x} vs e^{-x} and how they handle denominators with factors and parentheses.
3. Implement minimal changes in latex._print_Mul to adopt the pretty printer's grouping/ordering logic for sign, negative exponents, and denominator factor handling, preserving existing LaTeX-specific formatting where it improves readability.
4. Add/adjust unit tests where necessary (but do not create test creation tickets unless required). Ensure all existing latex tests continue to pass.

Planned tickets:
- 001_investigate_mul_printing.md: Investigate and document concrete differences between PrettyPrinter._print_Mul and LatexPrinter._print_Mul, with examples and suggested change points.
- 002_fix_latex_mul_grouping.md: Implement minimal patch for LatexPrinter._print_Mul to align grouping/ordering with PrettyPrinter._print_Mul.
- 003_fix_latex_piecewise_parentheses.md: Fix piecewise parentheses/closing when embedded in Mul or other contexts to match pretty printer.
- 004_code_review.md: Request code review for the implemented patches.
- 005_qa_validation.md: QA ticket to run the test suite, validate fixes, and report QA_VERDICT.

Assignment plan:
- I (Alice) will create the tickets and assign 002/003 to Engineer.
- Engineer will implement and push a patch, then signal for code review.
- CodeReviewer will review; if OK, they will transfer_to_QA.
- QA will run tests and provide QA_VERDICT.

Notes:
- The harness already applied the gold test patch. Implementation changes are default unless QA proves otherwise.
- Do not change test files.

Next step: create investigation ticket and assign to Engineer.
