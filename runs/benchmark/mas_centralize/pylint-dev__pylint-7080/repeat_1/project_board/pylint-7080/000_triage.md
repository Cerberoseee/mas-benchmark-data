Title: --recursive ignores ignore-paths

Summary:
When running pylint with --recursive=y and a pyproject.toml configuration containing ignore-paths patterns (e.g. "^src/gen/.*$"), paths passed as the current directory ("./...") are normalized with a leading './' and do not match the configured regex, so files under src/gen are still checked. The root cause is that the 'root' variable is not normalized before matching against self.config.ignore_paths in pylint/lint/pylinter.py. Using os.path.normpath on root (or otherwise normalizing path separators / removing leading './') will fix matching.

Repo: pylint-dev/pylint
Issue: pylint-dev__pylint-7080

Files/tokens:
- Failing test: tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir
- Related code: pylint/lint/pylinter.py around the path skipping logic
- Suggested fix: normalize the 'root' path (os.path.normpath) before matching against compiled ignore_paths regex list. Ensure cross-platform separator handling (Windows backslashes) is considered.

Constraints & notes:
- Minimal change surface: modify only the matching code to normalize root (or apply same normalization used when compiling ignore_paths) instead of broad redesign.
- Harness already applied gold test patch. Our job: implement change, run tests, hand off to QA and CodeReviewer per workflow.

Next steps:
1. Create focused tickets: implement fix, run unit tests (engineer), code review, QA verification.
2. Route to Engineer to implement fix.

