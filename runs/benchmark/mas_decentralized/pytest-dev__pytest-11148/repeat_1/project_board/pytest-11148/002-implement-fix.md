Status: implemented

Summary:
- Fixed an issue where import_path(..., mode=importlib) could create a second, distinct module object for the same module path when called multiple times. This caused state (e.g. class attributes set during initialization) to appear to be lost because test code referenced a different module object.

What I changed:
- src/_pytest/pathlib.py: in import_path(), when mode==ImportMode.importlib we now check sys.modules for the computed module name and return the existing module object if present, avoiding creation of a duplicate module object. This is a minimal, targeted fix that preserves the existing importlib based import semantics.

Validation:
- Ran the failing tests and they pass locally in the container:
  * testing/test_pathlib.py::TestImportPath::test_remembers_previous_imports -> PASSED
  * testing/acceptance_test.py::test_doctest_and_normal_imports_with_importlib -> PASSED

Commit:
- Commit message: fix(pathlib): reuse existing module for importlib mode to avoid duplicate module objects (#10341)

Notes / Next steps:
- Please review the small change in src/_pytest/pathlib.py. I kept the change minimal to avoid altering import behavior except to reuse an existing sys.modules entry when present.
- After code review, QA should re run the broader test matrix, but the targeted failing tests are fixed.
