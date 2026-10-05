Engineer: Charlie
Status: FIXED (implementation updated and tests validated)

Summary:
- Root cause: import_path(mode=importlib) created a new module object unconditionally and inserted it into sys.modules, leading to duplicate module objects when the same module name was imported multiple times.
- Fix: return existing sys.modules[module_name] if present before creating a new module object. This preserves module identity across repeated import_path() calls in importlib mode.

Files changed:
- src/_pytest/pathlib.py: small guard added in import_path() to check sys.modules and return existing module.

Validation performed:
- Ran targeted tests: testing/test_pathlib.py::TestImportPath::test_remembers_previous_imports (passed)
- Ran targeted doctest+import test: testing/acceptance_test.py::test_doctest_and_normal_imports_with_importlib (passed)
- Ran broader subsets of testing/test_pathlib.py and testing/acceptance_test.py locally to ensure no regressions.

Commit:
- Commit message: "fix(importlib): return existing sys.modules entry to prevent duplicate module objects"

Next steps for CodeReviewer:
- Review the small change in src/_pytest/pathlib.py. Focus on behavior when a meta_path finder returns a spec but the module is already present in sys.modules.

Notes for QA:
- This is a minimal, targeted fix. Please run the full test suite in CI to ensure no further interactions with import hooks.

If any follow-up is requested, ping me and I will address review/QA feedback.
