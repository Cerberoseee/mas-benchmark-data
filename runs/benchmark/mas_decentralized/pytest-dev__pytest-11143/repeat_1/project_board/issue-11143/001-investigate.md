Investigation task: confirm where rewrite.py checks for module docstring and why a numeric literal ends up as a docstring.

Steps:
- Inspect _pytest/assertion/rewrite.py for is_rewrite_disabled or similar function referencing docstring.
- Run quick local AST parse on a file with leading numeric literal to see what ast.get_docstring returns and what node types appear.
- Identify code path that does `if "PYTEST_DONT_REWRITE" in docstring` and guard against non-string docstrings.

Acceptance: short report capturing exact lines and a proposed minimal change (e.g. ensure docstring is str before using 'in').
