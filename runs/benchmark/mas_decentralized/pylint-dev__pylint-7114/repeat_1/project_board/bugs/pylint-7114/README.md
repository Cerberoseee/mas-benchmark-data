Title: Linting fails if module contains module of the same name

Issue: Running `pylint a` fails when directory `a/` contains a file `a.py` (same name as package), because pylint looks for a nonexistent a/__init__.py and errors. Should treat directory as namespace/package even without __init__.py or handle file shadowing.

Failing test: tests/lint/unittest_lint.py::test_identically_named_nested_module

Reproduction steps:
- Create directory a/ containing a.py and b.py (both empty)
- Run `pylint a` -> error: Unable to load file a/__init__.py

Notes:
- No patch yet. Next: triage sources where module resolution decides to look for __init__.py incorrectly when a module file exists with same name as package.
- Suspect importlib or astroid module loading logic, maybe in pylint.lint or astroid scoping of modules.
