Bug: autosummary: The members variable for module template contains imported members

Description
-----------
When rendering the autosummary module template, the template variable `members` includes imported members even when `autosummary_imported_members` is set to False in conf.py.

Repro
-----
1. Create a module `example.py` that imports `os`.
2. Use an autosummary template that iterates `members` and lists each item.
3. Set `autosummary_generate = True` and `autosummary_imported_members = False` in conf.py.

Observed: the generated module page lists `os` in `members`.

Expectation: imported members should be excluded from `members` when `autosummary_imported_members` is False.

Failing tests
-------------
- tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module
- tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module_skipped

Guiding principles
------------------
- Minimal change surface: fix generation of `members` variable when rendering autosummary module templates.
- Do not change test files.
- Typical path: Engineer -> CodeReviewer -> QA.
