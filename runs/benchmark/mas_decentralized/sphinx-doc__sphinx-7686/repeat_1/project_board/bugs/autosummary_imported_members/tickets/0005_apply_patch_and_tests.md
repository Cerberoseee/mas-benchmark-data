Status: Done

Summary:
Implemented a minimal fix to ensure the `members` template variable for module templates does not include imported members when `autosummary_imported_members` is False. The change filters the results of `dir(obj)` and only includes dunder names and locally-defined members discovered by autosummary when imported members are excluded.

Files changed:
- sphinx/ext/autosummary/generate.py

Testing performed:
- Ran the targeted fail-to-pass tests:
  - tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module  (PASSED)
  - tests/test_ext_autosummary.py::test_autosummary_generate_content_for_module_skipped  (PASSED)
- Ran the listed pass-to-pass tests from the task (all passed).

Commit:
Changes were committed to the local repository (see recent commit on branch master).

Notes for reviewer/QA:
- The fix is intentionally minimal and preserves existing behavior when `autosummary_imported_members` is True.
- The patch prefers a small whitelist of common dunder attributes to keep module metadata visible (e.g. __name__, __file__, etc.).

Ready for code review and QA validation.