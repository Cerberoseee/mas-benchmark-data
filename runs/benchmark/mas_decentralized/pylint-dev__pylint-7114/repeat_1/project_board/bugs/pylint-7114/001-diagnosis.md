Engineer task: Diagnose where pylint tries to open a/__init__.py when given directory a/ containing a.py.

Steps:
1. Run the failing test: pytest tests/lint/unittest_lint.py::test_identically_named_nested_module -q
2. Reproduce minimal case outside tests: create a/ with a.py and b.py, run `pylint a` and `pylint -E r a` per report.
3. Add logging or use debugger to trace where the path 'a/__init__.py' is constructed and passed to open/astroid.parse.
4. Inspect code in modules:
   - pylint.lint
   - pylint.utils
   - pylint.utils.module_utils
   - pylint.reporters
   - astroid.builder or astroid.manager used by pylint
5. Identify the function that maps file paths to module names and decides to use __init__.py.
6. Propose minimal code change: if package dir contains module file with same base name, prefer parsing that (.py) file instead of non-existent __init__.py.

Deliverables:
- Location of responsible code and a short explanation why it tries to open a/__init__.py
- Suggested minimal patch (diff) to change behavior
- Run tests and capture failures
