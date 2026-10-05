Title: Set default FILE_UPLOAD_PERMISSIONS to 0o644

Issue: django#10914 (SWE-bench reproduction)

Summary:
The project's tests indicate a failing test related to overriding FILE_UPLOAD_PERMISSIONS default behavior. The requested change in the upstream issue is to change default FILE_UPLOAD_PERMISSIONS from None to 0o644 and update docs and release notes accordingly.

Goal:
- Implement minimal code change to set FILE_UPLOAD_PERMISSIONS default to 0o644 where appropriate.
- Update tests that assume the old default to reflect the new default.
- Add a breaking-change note in releases/2.2.txt.
- Run tests for the failing suite and validate.

Constraints and strategy:
- Keep change surface minimal: only change default value, tests, and doc/release note references.
- Do not change FILE_UPLOAD_DIRECTORY_PERMISSIONS default (discussion in issue suggests leave it as-is).
- Ensure tests updated are only those that intentionally rely on previous default behavior.
- Engineer -> QA -> ProjectManager flow.

Planned tickets:
1. 001_update_default_setting: Change default FILE_UPLOAD_PERMISSIONS value in settings to 0o644 and update related constant/usage.
2. 002_update_tests: Modify tests that assert previous default to use new default or adjust expectations.
3. 003_add_release_note: Add breaking change note to releases/2.2.txt.
4. 004_docs_update: Update settings/docs references (optional in SWE-bench if docs present).
5. 005_run_tests_and_fix: Run failing tests and iterate.

Routing:
- Assign 001_update_default_setting and 002_update_tests to Engineer.
- After patch is produced, forward to CodeReviewer if diff shape needs review, then to QA for test run.

Next steps:
- Transfer to Engineer to implement 001 and 002.