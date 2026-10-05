Title: 001_diagnose - Locate failing code and tests
Owner: Engineer

Tasks
- Run failing test: model_fields.test_filepathfield.FilePathFieldTests::test_callable_path
- Inspect implementation of FilePathField (django/db/models/fields/files.py or models/fields/__init__.py?) and form field (django/forms/fields.py - FilePathField). Determine where path is used and when evaluation must happen.
- Confirm migration serialization already handles callables (likely uses deconstruct that returns import path); ensure not to modify migration logic.

Acceptance
- Identify exact lines where TypeError arises and propose minimal change: evaluate callable at appropriate earliest point. Document findings in ticket.
