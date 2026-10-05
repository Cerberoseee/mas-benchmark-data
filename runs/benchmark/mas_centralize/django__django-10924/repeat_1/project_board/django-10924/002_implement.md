Title: 002_implement - Evaluate FilePathField.path if callable
Owner: Engineer

Summary
- Implement logic to accept callable for FilePathField.path and evaluate it to a string path where the rest of the code expects a string.
- Candidate locations: FilePathField.__init__ in django/db/models/fields/files.py or the form field django/forms/fields.py at beginning of the form field __init__ when path variable is still possibly callable.

Tasks
- Modify the model field so that if path is callable, the field keeps the original callable for deconstruct() but ensures the form field and widget receive a resolved string path at runtime. Approach: store the callable in self._path_callable and expose a property self.path that resolves to self._path_callable() when accessed. Alternatively, in __init__, if callable(path) set self._path_callable = path and set self.path = path() while keeping deconstruct to return import path — careful to keep migrations serialization using import path (i.e., if original argument was callable, deconstruct should return the import path string, not the evaluated path).
- Update forms.FilePathField to resolve callable paths if passed.
- Run tests.

Acceptance
- test_callable_path passes, existing tests unaffected.

Notes
- Keep changes minimal and add comments explaining why resolving is deferred and how deconstruct keeps callable import path.
