T1 - Diagnose: locate regex parsing and compilation

Objective:
Find where pylint parses config options that are regexes and where re.compile is called so we can add appropriate error handling.

Acceptance criteria:
- Path(s) to relevant code identified (file and function/class).
- Short note describing how regex options are currently processed.
- Reference to failing tests that exercise the code paths.

Assignee: Engineer