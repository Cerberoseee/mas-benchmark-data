Engineer ticket: Diagnose and fix failing test_identically_named_nested_module

Goal: Fix tests/lint/unittest_lint.py::test_identically_named_nested_module so that
pylint correctly handles a directory that contains a module with same name (a/a.py)
as a namespace package and does not attempt to load a/__init__.py.

Steps:
1. Run the failing test locally (or rely on harness). Open tests/lint/unittest_lint.py
   and inspect test_identically_named_nested_module to understand expectations.
2. Search the codebase for module/package discovery logic in pylint.lint or astroid
   integration that determines when to look for __init__.py. Candidate modules:
   - pylint.lint
   - pylint.utils
   - pylint.reporters
   - astroid.builder or AstroidManager integration
3. Reproduce the error path where Pylint constructs a module node for 'a' and tries
   to load a/__init__.py. Identify minimal change to avoid treating 'a' as a package
   requiring __init__.py when a/a.py exists.
4. Implement a focused change with an explanatory comment and tests if needed.
   Prefer modifying only the implementation code touched by tests.
5. Run pytest for the failing test and related import tests.
6. Commit changes; produce a patch (read_patch_diff will capture it).

Deliverables:
- Patch that fixes the failing test without breaking the pass-to-pass tests.
- Short note in the commit message explaining the rationale.

Notes:
- If you find the issue is in astroid, consider adding a guard to prefer modules over packages when a module file exists with the same name.
- If the implementation changes affect module resolution ordering, ensure no regressions.

