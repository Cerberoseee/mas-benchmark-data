Title: Module imported twice under import-mode=importlib

Repository: pytest-dev/pytest
Issue: failing tests when import-mode=importlib causes modules to be imported twice under certain conditions (doctest-modules + module importing another module). Matches reporter's finding and similar to #10341.

Goal: Diagnose and fix the cause so tests pass. Keep change surface minimal.

Background:
- Failing tests: testing/test_pathlib.py::TestImportPath::test_remembers_previous_imports, testing/acceptance_test.py::test_doctest_and_normal_imports_with_importlib
- The issue appears when using importlib import-mode and doctest-modules; a module can be imported twice with two distinct module objects in sys.modules.
- Reporter provided a minimal reproducer; suspect import hook handling for doctest-module collection path causing import path normalization mismatch.

Plan:
1) Reproduce locally (run failing tests) to observe stack traces.
2) Inspect importlib-mode related code (pytest's import handling, pymod importers). Focus on test collection logic for doctest-modules and import hook behavior.
3) Identify scenario where two different module specs/keys are used to import same file (e.g., package-relative vs file path causing different module name or path).
4) Implement minimal fix: ensure the importer maps module to canonical name and reuses existing sys.modules, or normalize module name before import, or prefer importlib.util.spec_from_file_location with package argument.
5) Add tests to capture regression.
6) Run the failing tests and full suite subset.

Tickets to create:
- 001-diagnose.md -> investigate and propose patch
- 002-implement-fix.md -> implement small patch in import machinery
- 003-code-review.md -> request review
- 004-qa.md -> testing instructions & QA verification

Assignees: Engineer (you), CodeReviewer, QA.

Notes:
- Must follow SWE-bench flow: Engineer implements, then CodeReviewer reviews, then QA validates. Each step should use transfer_to_* tools.
- Keep patch minimal; do not rewrite import machinery broadly.
