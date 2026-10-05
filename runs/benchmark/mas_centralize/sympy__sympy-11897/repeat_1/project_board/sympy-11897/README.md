Issue: LaTeX printer inconsistent with pretty printer
Repo: sympy/sympy
Base commit: e2918c1205c47345eb73c9be68b14c0f15fdeb17

Goal: Make LaTeX printer produce output consistent with PrettyPrinter for Mul and Piecewise cases described in the issue, minimizing surface changes.

Workflow:
- Triage and reproduce failing test(s)
- Create small implementation ticket(s)
- Assign to Engineer to implement minimal fix
- Hand off to CodeReviewer if needed
- Hand off to QA for testing
- Close when QA verifies and patch exists

Notes:
- Tests failing: test_latex_Piecewise
- Many latex tests pass; avoid regressions
- Do not change tests; implementation-only changes expected
