Title: Fix missing parentheses in LaTeX printing of Piecewise expressions

Description:
Investigate and fix LaTeX printing of Piecewise when it is embedded in Muls or other contexts where the pretty printer produces surrounding parentheses but the LaTeX printer omits them. Ensure Piecewise prints with parentheses when needed to preserve precedence and match pretty printer's structure.

Assignee: Engineer
Priority: Medium

Acceptance criteria:
- Implemented patch committed.
- Tests related to piecewise latex printing (test_latex_Piecewise) now pass.
- Request code review after implementation.
