Engineer ticket: make QDP command parsing case-insensitive

Description
-----------
Adjust the QDP reader so command detection is case-insensitive. The failing
unit test indicates that lines like `read serr 1 2` are not recognized. Two
approaches acceptable (choose one):
- Use re.IGNORECASE in regex compilation wherever commands are matched; or
- Normalize input lines to upper-case before matching (careful to preserve
  data rows which are numeric).

Recommended change
------------------
In astropy/io/ascii/qdp.py, locate the regex(es) used to detect QDP command
lines and compile them with the re.IGNORECASE flag (e.g., re.compile(...,
re.IGNORECASE)). This keeps payload unchanged and is minimal.

Acceptance criteria
-------------------
- The failing test astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]
  passes.
- Other qdp tests remain passing.
- No change to test files.

Notes
-----
- Provide a patch via the repository (commit). After patching, handoff to QA
  for running the test suite.
