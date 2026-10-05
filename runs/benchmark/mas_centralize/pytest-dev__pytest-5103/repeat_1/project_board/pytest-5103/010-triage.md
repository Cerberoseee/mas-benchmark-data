Triage notes:

Failing test is about assertion rewriting unrolling expressions for all/any.
The assertion rewriter is in _pytest/assertion/rewrite.py (or rewrite_ast.py in older versions). We need to find the AST transform that handles calls and generator/list comprehensions.

Plan:
- Create tickets:
  - Implement: Update assertion rewrite AST transformer to detect all()/any() with a generator/list/tuple comprehension or generator expression and replace with an unrolled for-loop assert per element.
  - Tests: Ensure existing failing test passes and run the assertion rewrite test suite subset.
  - Code Review: Quick pass from reviewer.
  - QA: Run pytest tests and validate failing test passes.

Next: Assign to Engineer to implement minimal change.