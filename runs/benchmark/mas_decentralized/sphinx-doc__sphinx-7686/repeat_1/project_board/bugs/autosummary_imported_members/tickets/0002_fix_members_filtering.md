Title: Fix: Exclude imported members from `members` when autosummary_imported_members is False

Description:
Once the investigation identifies the code location, implement a minimal change so that when generating module autosummary pages, the `members` template variable does not include imported members if the config option `autosummary_imported_members` is False.

Requirements:
- Modify the code path that builds `members` for modules.
- Ensure other autosummary behaviors/tests are unaffected.
- Add/adjust unit tests only if strictly necessary (prefer to rely on existing tests).

Acceptance criteria:
- A non-empty patch is produced that changes implementation code.
- All autosummary tests pass, especially the two previously failing tests.

Assignee: Engineer
Labels: bug, fix, autosummary
