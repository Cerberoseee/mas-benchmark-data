Title: Module imported twice under import-mode=importlib (pytest-11148)

Summary:
- Tests failing in importlib import-mode where a module (e.g., pmxbot.logging) gets imported twice under different module objects, causing initializer side-effects to apply to one object while tests reference another.
- Two failing tests in the pytest repo reproduction: testing/test_pathlib.py::TestImportPath::test_remembers_previous_imports and testing/acceptance_test.py::test_doctest_and_normal_imports_with_importlib
- The issue appears related to importlib hook path handling and doctest-modules interaction; possibly same as #10341.

Scope:
- Repository: pytest-dev/pytest
- Base commit: 2f7415cf
- Failing conditions only reproduce when import-mode=importlib and doctest-modules is used and a module imports another module.

Goals:
- Identify root cause in importlib import mechanism inside pytest's import hooks.
- Implement minimal fix so a module is not double-imported (ensure sys.modules identity used consistently).
- Add/adjust tests if needed (but harness indicates gold test patches already applied).

Constraints & strategy:
- Minimal surface change to core import path/loader handling.
- Keep team handoffs: Engineer to implement patch, CodeReviewer if needed, QA to validate failing tests pass.

Next actions:
- Create focused tickets: diagnosis, implementation, code review, QA.
- Transfer to Engineer to implement fix (required by SWE-bench rules).