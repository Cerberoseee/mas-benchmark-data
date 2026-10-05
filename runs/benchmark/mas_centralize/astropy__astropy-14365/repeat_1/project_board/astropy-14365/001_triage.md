Triage notes
============

Files to inspect
----------------
- astropy/io/ascii/qdp.py (likely location)
- astropy/io/ascii/tests/test_qdp.py (tests already reveal failing case)

Failing test
------------
- astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]

Hypothesis
----------
The QDP format parser matches command lines using a regex that expects upper-case
commands. Changing the regex to be case-insensitive should fix the issue.

Next steps
----------
- Create an Engineer ticket to implement a small change in the QDP parser to
  make regex matching use re.IGNORECASE or normalize lines to upper-case before
  matching.
- Keep the rest of logic unchanged to minimize risk.
