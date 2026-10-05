Title: Implement normalization for ignore-paths matching when running recursively

Description:
Failure: ignore-paths regex patterns do not match when root path contains leading './' or OS-specific separators; e.g. when running `pylint --recursive=y .` and ignore-paths contains "^src/gen/.*$", compiled regex won't match './src/gen' path.

Goal: Normalize paths used for matching (root variable) before testing against compiled ignore_paths. Keep the change minimal and targeted in pylint/lint/pylinter.py where the skip logic occurs.

Acceptance criteria:
- Unit test tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir passes.
- No regression in the listed pass-to-pass tests (particularly recursive/ignore_pattern tests).
- Change limited to minimal lines, with clear comment and cross-platform-safe normalization (os.path.normpath and possibly os.path.abspath or stripping leading './').

Implementation notes:
- Where root is compared to entries in self.config.ignore_paths (compiled regex list), normalize root with os.path.normpath(root) or equivalent and use forward/backslash-insensitive matching (regex already contains alternation for backslash vs forward slash).
- Consider also normalizing paths at config parsing time, but prefer minimal, local fix in p y l i n t e r . p y to avoid impacting other code.

Files to modify:
- pylint/lint/pylinter.py

Estimate: 1-2 hours

Please implement and commit changes, then notify CodeReviewer for review and QA for test run.
