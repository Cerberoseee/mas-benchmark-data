Title: Add __version_info__ to top-level matplotlib

Summary:
User requested exposing a comparable version representation in addition to __version__ (string). Tests failing indicate new utility parse_to_version_info behavior is expected. We need to add __version_info__ to matplotlib top-level, likely in lib/matplotlib/__init__.py or version parsing utility, using a tuple similar to sys.version_info.

Scope:
- Implement __version_info__ export at top-level in a way that the existing tests expect.
- Keep change surface minimal: add parsing helper and set __version_info__ only.
- Ensure no test files are modified.

Initial findings:
- Four tests in lib/matplotlib/tests/test_matplotlib.py::test_parse_to_version_info are failing. They expect parsing of versions like "3.5.0", "3.5.0rc2", "3.5.0.dev820+g...", "3.5.0.post820+g..." to map to certain tuples.
- The harness applied gold tests; engineer patch not present yet.

Next steps (tickets):
1) Engineer: Implement parsing utility and set __version_info__ in lib/matplotlib/__init__.py. Small focused change.
2) Code Review: Review the patch for correctness and minimality.
3) QA: Run tests and validate the failing tests are now passing. Provide QA_VERDICT.

Assignments and order: Engineer -> CodeReviewer -> QA -> ProjectManager

Notes:
- Ensure that parse handles rc, dev, and post versions as expected by tests.
- Confirm read_patch_diff shows non-empty patch before declaring completion.
