QA ticket: validate QDP case-insensitivity fix

Objective
---------
Run the test suite for ASCII QDP and verify the failing test now passes and no
regressions are introduced.

Tests to run
------------
- Run pytest -k qdp or specifically:
  astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]
  and the entire astropy/io/ascii/tests/test_qdp.py file.

Expected QA_VERDICT block
-------------------------
Provide a QA_VERDICT block with:
- verified: true/false
- If false, include failing_ids and notes explaining failures.

Notes for QA
------------
If any failures indicate collection issues or tests not found, inform the
Engineer: "Test cases are auto-applied by the harness — do not write them
yourself..." per project instructions.
