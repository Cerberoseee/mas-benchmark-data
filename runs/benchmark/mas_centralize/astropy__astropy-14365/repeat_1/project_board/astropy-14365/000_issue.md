Title: QDP parser should accept lower-case commands

Repository: astropy/astropy
Issue: ascii.qdp Table format assumes QDP commands are upper case

Problem
-------
The ascii.qdp reader currently expects QDP commands (like `READ SERR`) to be
upper-case. QDP itself is case-insensitive and many real-world files use lower
or mixed case. This causes parsing to fail on files like:

read serr 1 2 
1 0.5 1 0.5

which should be parsed and produce a Table with errors.

Root cause
----------
The regex used to detect QDP commands is not case-insensitive, so lines with
lower-case commands are not recognized.

Goal
----
Make the QDP command parsing case-insensitive with minimal change surface so
existing behavior is preserved.

Constraints
-----------
- Only change implementation; tests are already provided by harness.
- Keep changes minimal and focused to avoid regressions.

Plan
----
1. Triage and locate the QDP reader implementation.
2. Create a small patch to make command regex matching case-insensitive.
3. Run tests (focus on failing test).
4. Iterate if QA reports failures.

Deliverables
------------
- Patch that adjusts regex to be case-insensitive.
- Engineer handoff with patch applied.
- QA validation that failing test passes and others stay green.
- Final summary and project completion.
