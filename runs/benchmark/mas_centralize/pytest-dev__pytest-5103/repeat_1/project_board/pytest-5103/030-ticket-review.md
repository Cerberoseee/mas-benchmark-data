Ticket: Code review for assertion rewriter all/any unroll

Description:
Review the engineer's patch for correctness, minimality, and potential AST edge-cases.

Checklist:
- Ensure transformations don't change runtime behavior beyond reporting.
- Check for preserving side effects ordering.
- Look for introduced syntax errors in edge cases.
- Check test coverage added/updated.

Assignment: CodeReviewer role.