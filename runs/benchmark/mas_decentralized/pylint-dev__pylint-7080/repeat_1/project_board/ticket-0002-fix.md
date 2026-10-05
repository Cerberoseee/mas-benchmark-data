Ticket: 0002-fix - Normalize root path when checking ignore-paths

Status: IMPLEMENTED (awaiting review)

Engineer notes:
- Implemented minimal change in pylint/lint/expand_modules.py to normalize candidate paths before matching against ignore-paths regexes.
- Normalization steps:
  - os.path.normpath(element) to remove leading './' and normalize separators
  - replace os.path.sep with '/' to ensure regexes authored with forward slashes match on all platforms
  - use os.path.basename(normalized) for basename checks
- Patch file: pylint/lint/expand_modules.py

Local test results (run by Engineer):
- pytest tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir -> PASS
- pytest tests/test_self.py::TestRunTC::test_ignore_path_recursive -> PASS

Next: hand off to CodeReviewer for review.

Patch summary (git):
commit 1507246d78f462787cc219653649ba4526ca539f
Author: Engineer
Date: (recorded by harness)

    Fix: normalize paths when checking ignore-paths to handle leading ./ (issue 7080)

Files changed:
- pylint/lint/expand_modules.py

Acceptance criteria for reviewer:
- Confirm change is minimal and correct.
- Confirm use of os.path.normpath + separator normalization is acceptable and doesn't alter semantics for other ignore-paths uses.
- If accepted, transfer to QA.
