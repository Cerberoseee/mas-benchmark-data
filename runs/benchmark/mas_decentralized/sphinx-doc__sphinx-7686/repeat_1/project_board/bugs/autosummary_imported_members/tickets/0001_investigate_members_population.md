Title: Investigate how `members` is populated for module templates in autosummary

Description:
Investigate the code path that builds the `members` variable passed to the autosummary module template. Determine where imported members (e.g., `os`) are included even though config `autosummary_imported_members` is False.

Acceptance criteria:
- Identify the function(s) responsible for populating `members` for modules.
- Find why imported members are included despite config setting.
- Propose minimal code change(s) to exclude imported members based on `autosummary_imported_members`.

Assignee: Engineer
Labels: bug, investigation, autosummary
