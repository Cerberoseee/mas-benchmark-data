Title: bug/inspect-autosummary-members

Goal: Find the code path in sphinx.ext.autosummary that constructs the `members` variable for module templates and identify why imported members are included despite autosummary_imported_members=False.

Acceptance criteria:
- File(s) and functions responsible for building `members` located.
- Short explanation of how autosummary_imported_members is expected to be applied and where it currently isn't.
- Reproducer steps and quick local verification command(s) (pytest target).

Assignee: Engineer
Labels: bug, autosummary

Steps:
1. Search for autosummary implementation files (sphinx/ext/autosummary).
2. Locate code creating context for templates (likely TemplateBridge or Autosummary class).
3. Inspect handling of imported members vs. module members and config option autosummary_imported_members.
4. Run failing tests to reproduce.
