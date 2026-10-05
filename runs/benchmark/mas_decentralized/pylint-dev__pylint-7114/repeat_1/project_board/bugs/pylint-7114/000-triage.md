Title: Triage - Linting fails if module contains module of the same name

Summary:
Running `pylint a` fails when directory `a/` contains a file `a.py` (same name as package), because pylint looks for a nonexistent a/__init__.py and errors. Should treat directory as package/namespace package even without __init__.py, or avoid falsely trying to parse a/__init__.py when a/a.py exists.

Failing test:
- tests/lint/unittest_lint.py::test_identically_named_nested_module

Reproduction:
- Create directory a/ with files a.py and b.py (both empty)
- Run `pylint a` -> error: Unable to load file a/__init__.py: [Errno 2] No such file or directory: 'a/__init__.py'

Initial hypothesis / focus areas:
- The problem looks like module resolution logic that, when given a directory path that contains a module file with the same basename as the directory, constructs an import path that ends up mapping to a/__init__.py and tries to parse it.
- Likely places to inspect:
  - pylint's entrypoint / lint runner (pylint.lint) where it builds the list of modules to analyze from the given path arguments
  - utility functions that compute module names from file paths (pylint.utils or pylint.utils.module_utils)
  - interaction with astroid's module loading / package vs module resolution logic (astroid.builder or astroid.manager)

Constraints:
- Minimal surface change preferred: fix module-name detection/lookup logic to prefer actual files when a directory contains a same-named file, and avoid attempting to load a/__init__.py unless it exists.
- Tests are provided; ensure the patch makes the failing test pass without regressing the listed pass-to-pass tests.

Next actions:
- Create diagnosis task for Engineer to run failing test locally and locate the code path that generates the attempt to open a/__init__.py.
- After diagnosis, create implementation ticket with proposed change and tests.
