Issue: Linting fails if module contains module of the same name (pylint #7114)

Repository: pylint-dev/pylint
Base commit: 397c1703e8ae6349d33f7b99f45b2ccaf581e666

Failure: tests/lint/unittest_lint.py::test_identically_named_nested_module

Summary:
When a package directory contains a module file with the same name (e.g., a/a.py)
and no __init__.py, running `pylint a` incorrectly attempts to load a/__init__.py
and errors with "Unable to load file a/__init__.py: [Errno 2] No such file or directory".
Expected behavior is to treat a as a namespace package and successfully analyze
submodules such as a.b.

Plan:
- Reproduce failing test locally (harness will run tests). Identify where discovery
  treats a as a package requiring __init__.py when it should be a namespace package.
- Make minimal implementation change to avoid looking for __init__.py when a module
  with same name exists.
- Add unit tests / ensure existing tests pass.

Constraints / Notes:
- Don't rewrite whole import system. Prefer small change in module discovery.
- Ensure other tests that depend on package behavior still pass.

Next steps:
1. Engineer: inspect failing test and project source, produce focused patch.
2. CodeReviewer: review patch for correctness and minimal surface.
3. QA: run test suite for the failing test and related tests.

