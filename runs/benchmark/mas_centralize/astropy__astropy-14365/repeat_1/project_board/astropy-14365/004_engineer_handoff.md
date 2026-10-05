Engineer handoff

I made a minimal patch to astropy/io/ascii/qdp.py to make QDP command
recognition case-insensitive and to handle the 'NO' token case-insensitively
when parsing data values.

Patch summary:
- Compile the QDP line-type regex with re.IGNORECASE so commands like
  'read serr' or 'Read SERR' are recognized.
- Use v.upper() == 'NO' when parsing data values to treat 'no', 'No', etc., as
  masked values.

Commit: ebf9b0e36d4aa4bb1a54103c67d9cd5376b93ed7

Tests run:
- The specific failing test astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]
  passed locally in the engineer run.
- Several related qdp tests also passed.

Next step: Please run QA validation of the qdp test suite (see QA ticket).
