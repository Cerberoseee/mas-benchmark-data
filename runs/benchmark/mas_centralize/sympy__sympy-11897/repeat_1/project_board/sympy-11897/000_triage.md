Triage notes

Failing tests: test_latex_Piecewise (fail-to-pass)

Likely cause:
- Difference between PrettyPrinter._print_Mul and LatexPrinter._print_Mul; Latex may omit grouping/parentheses or factor 1 into denominator differently.
- Piecewise printing lacks correct parentheses around cases in some contexts.

Action plan (tickets):
1. TICKET-001 reproduce_and_add_debug: Add minimal reproducer tests (if not already present) and run targeted diagnostics to capture exact failing output. (Engineer)
2. TICKET-002 align_mul_printing: Modify LatexPrinter._print_Mul to match grouping and multiplication/denominator formatting from PrettyPrinter._print_Mul, ensuring minimal change set and preserving LaTeX-specific improvements only when superior. (Engineer)
3. TICKET-003 piecewise_parentheses: Ensure Piecewise printing in LatexPrinter adds parentheses when needed, matching pretty printer behavior. (Engineer)
4. TICKET-004 review_changes: Code review of diffs focusing on correctness and test coverage. (CodeReviewer)
5. TICKET-005 qa_validate: Run full latex test suite and targeted failing test; provide QA_VERDICT. (QA)

Dependencies:
- TICKET-002 and TICKET-003 can be done in the same patch if small, but separate changes help pinpoint regressions.

Notes on approach:
- Prefer reproducing failing test_latex_Piecewise and adjusting LatexPrinter._print_Piecewise and _print_Mul
- Do not edit tests; only implementation
- Run pytest --collect-only if tests fail to collect
