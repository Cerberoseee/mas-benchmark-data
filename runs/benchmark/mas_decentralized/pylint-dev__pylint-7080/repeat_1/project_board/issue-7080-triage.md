Title: --recursive=y ignores ignore-paths (issue #7080)

Summary:
When running pylint with --recursive=y and giving a path like '.', configured ignore-paths are not applied because the root path string includes a './' prefix (e.g. './src/gen'), so existing regexes like '^src/gen/.*$' don't match. This causes generated files under src/gen to be checked unexpectedly.

Root cause hypothesis:
The code that decides whether to skip a path compares the given root path string against compiled ignore-paths regexes directly. The path is not normalized (leading './' and platform path separators), so valid ignore-path regexes don't match in some invocation styles (notably when the argument is '.'). Normalizing the path with os.path.normpath before matching should fix this.

References:
- Affected file: pylint/lint/pylinter.py (decision of skipping path near check for self.config.ignore_paths)
- Failing test: tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir
- Related PR: https://github.com/PyCQA/pylint/pull/6528

Suggested minimal fix:
Normalize the root path (os.path.normpath(root)) before running it through the ignore-paths regex checks. Keep change localized to the single comparison; avoid wider refactors.

Tickets created:
- 0001-diagnose: reproduce and confirm failure locally
- 0002-fix: implement normalization fix and run unit tests
- 0003-review: code review of the change
- 0004-qa: validate fix against the failing test and a small reproduction on Windows-style paths

Notes for engineer:
- The harness already applied the failing test. Do not touch test files.
- Run the single failing test first: pytest tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir -q
- Implement minimal change in pylint/lint/pylinter.py: normalize the root path with os.path.normpath before checking ignore_paths. Ensure the change doesn't alter behavior for previously passing tests.
- After implementing, run the test suite (or at least the self tests listed in the board ticket) and produce the patch (read_patch_diff will be used by triage once you hand off).

Owner: Alice (project manager)
