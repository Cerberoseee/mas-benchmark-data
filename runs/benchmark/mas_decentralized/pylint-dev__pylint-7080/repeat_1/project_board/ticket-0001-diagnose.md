Ticket: 0001-diagnose - Reproduce and confirm failure

Goal:
Reproduce the failing test tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir and gather debug logs showing root and compiled ignore_paths for both invocation styles (pylint src/ and pylint .).

Acceptance criteria:
- Local run of the failing test demonstrates the failure.
- Collect pdb/logging prints showing root strings and regex patterns used for matching.

Steps for Engineer:
1. Run the failing test directly to ensure it fails: pytest tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir -q
2. Add temporary debug prints (or run under pdb) in pylint/lint/pylinter.py where the ignore_paths matching occurs to print `root` and `self.config.ignore_paths` when invoked for both `src/` and `.` to confirm presence of './' prefix.
3. Save logs and attach them to this ticket.

Notes:
- Do not commit debug prints to the repository; keep changes local for diagnosis. We'll implement the fix in a separate ticket.
- If reproduction fails on the developer machine, run `pylint --recursive=y .` manually on a small repro (create src/gen/test.py as described in the issue).

Estimate: 1-2 hours
Assignee: Engineer
