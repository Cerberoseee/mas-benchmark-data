Title: Allow FilePathField.path to accept a callable (deferred evaluation)

Issue summary

FilePathField currently supports writing a callable as the "path" argument in model definitions so makemigrations can store the import path of the callable in migrations. However, at runtime (forms and model field instantiation) the FilePathField and/or its form field expect path to be a string and run os.scandir()/string ops on it, causing TypeError when a callable has been provided. This forces developers to manually edit migrations or to avoid using environment-dependent settings when building path strings.

Goal

Make FilePathField accept a callable for path and evaluate it lazily (at runtime where appropriate) so:
- makemigrations continues to store the import path of the callable in migrations
- instantiating the model field and form works without TypeError
- minimal changes to public API and migration format

Scope and constraints

- Minimize change surface: implement evaluation of callable early during runtime initialization of the field or its form counterpart where safe (models.Field.__init__ occurs at class import time, so careful about evaluating too early)
- Preserve existing behavior when path is a string
- Ensure tests cover the failing case and existing path tests still pass

Files likely affected

- django/db/models/fields/files.py (FilePathField implementation)
- django/forms/fields.py (form FilePathField interacting code is in forms.fields.FilePathField or ChoiceField creation code)
- Tests: django/tests/model_fields/test_filepathfield.py (add/modify test_callable_path)

Proposed approach

1. In Model Field: do NOT evaluate callable in FilePathField.__init__ (keeps migration serialization intact). Migration machinery relies on storing the callable import path.

2. In Form Field: evaluate callable at the beginning of the form field __init__ (or where the path is used to build choices). The form needs a string path for os.scandir and path manipulations.
   - Look for where forms.FilePathField or ModelChoiceField uses the model field's path attribute and coerce callables to string: if callable(path): path = path()

3. Add a test that creates a model with FilePathField(path=callable) and runs the code path exercised by the existing failing test test_callable_path.

Tasks

- Triage and confirm failing tests locally (CI harness already shows test_callable_path failing)
- Implement change in forms.fields to evaluate callable path early (and also guard other uses of path in code that assume string)
- Run tests
- Prepare small patch and request Code Review
- After review, route to QA for verification

Deliverables

- Small patch + tests
- Tickets for Engineer -> CodeReviewer -> QA

References

- Django ticket: https://code.djangoproject.com/ticket/6896
- Related PRs: PR#10299, PR#10924 (community discussion)

Estimated effort

Small: ~2-4 hours to implement + tests + review.
