Title: Allow FilePathField path to accept a callable
Repo: django/django
Issue: django ticket #10924 (SWE-bench instance)

Problem
- FilePathField.path is evaluated at import/field init time when it may be a callable returning a path based on environment (e.g. settings.LOCAL_FILE_DIR). makemigrations resolves the path into a hardcoded absolute path, causing migrations to record machine-specific paths and break on other environments.
- Tests show one failing test: test_callable_path in model_fields.test_filepathfield.FilePathFieldTests.

Goal
- Allow FilePathField to accept a callable for path, storing the dotted import path in migrations and evaluating the callable at runtime where appropriate so forms and field cleaning work.

Constraints
- Minimal surface changes; prefer small targeted patches.
- Must include Engineer and QA handoffs in flow.

Plan
1. Reproduce failing test and inspect current implementation.
2. Modify FilePathField and related form field to accept callable path; ensure callable import path is serialized in migrations (likely already handled) and evaluation occurs where needed (forms or model field init) so code that expects a string path sees a string.
3. Add/adjust tests if necessary (assume harness applied gold test patch).
4. Run tests; iterate until QA passes.

Tickets to create
- 001_diagnose: Reproduce failure and locate code paths (models/fields and forms/fields usage)
- 002_implement: Implement callable path evaluation in the minimal correct place(s)
- 003_review: Code review
- 004_qa: Run test suite for the failing test and validate

Routing
- Engineer: implement 002 (transfer_to_engineer)
- After patch, CodeReviewer: review (transfer_to_codereviewer) if needed
- QA: run tests (transfer_to_qa)

Notes
- Read the original PRs (10299, 10924) for context; they suggest evaluating callable in field init or forms field init.
- Ensure not to change tests; harness applied gold patch.
