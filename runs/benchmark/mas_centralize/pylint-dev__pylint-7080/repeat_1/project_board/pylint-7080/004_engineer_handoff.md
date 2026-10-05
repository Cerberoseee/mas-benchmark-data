Engineer handoff

Engineer implemented minimal fix in pylint/lint/pylinter.py to normalize discovery root before matching ignore_paths. Patch summary:
- Introduced normroot = os.path.normpath(root)
- Used normroot.startswith(s) for skip_subtrees matching
- Passed os.path.normpath(root) + os.sep into _is_ignored_file to ensure trailing separator and normalized path when matching ignore configs.

Patch diff (abbreviated):
- if any(root.startswith(s) for s in skip_subtrees):
+ normroot = os.path.normpath(root)
+ if any(normroot.startswith(s) for s in skip_subtrees):
...
- _is_ignored_file(root, ...)
+ _is_ignored_file(os.path.normpath(root) + os.sep, ...)

Engineer ran failing test and it passed locally:
- tests/test_self.py::TestRunTC::test_ignore_path_recursive_current_dir => PASSED

Next: code review, then QA verification.
