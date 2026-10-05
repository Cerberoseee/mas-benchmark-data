Ticket: EN-0001
Title: Implement case-insensitive QDP command matching in ascii.qdp

Description:
The QDP reader currently expects uppercase commands and fails on lower-case commands. Update the reader so command detection is case-insensitive.

Acceptance criteria:
- Tests pass, including astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]
- No changes to test files.
- The change surface is minimal (ideally a single small change in the qdp reader).

Implementation notes:
- Prefer using re.IGNORECASE on the regex used to find QDP commands rather than converting input lines to upper-case (to preserve tokens).
- Search in astropy/io/ascii/src or similar for ascii.qdp reader; suggested file: astropy/io/ascii/qdp.py or astropy/io/ascii/core.py (discover exact path).
- Run pytest for the qdp tests.

Estimate: 1-2 hours

Assignee: Engineer

Steps:
1. Locate the qdp reader implementation.
2. Modify regex compilation to include IGNORECASE (or use case-insensitive matching) where QDP commands are detected.
3. Run tests and iterate if needed.
4. Commit changes and push patch for review.

Linked tickets: CR-0001, QA-0001
