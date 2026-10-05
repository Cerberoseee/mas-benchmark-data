Title: ascii.qdp Table format assumes QDP commands are upper case

Summary:
The QDP reader in astropy.io.ascii.qdp currently treats QDP commands as case-sensitive and expects upper-case commands (e.g., "READ SERR 1 2"). QDP itself is case-insensitive; lower-case commands like "read serr 1 2" should be accepted. This causes a ValueError when reading well-formed QDP files that use lower-case commands.

Reproduction:
- A QDP file with "read serr 1 2" fails to parse, raising ValueError: Unrecognized QDP line: read serr 1 2

Scope:
- Unit tests indicate one failing test: astropy/io/ascii/tests/test_qdp.py::test_roundtrip[True]
- Several other qdp tests pass.

Root cause hypothesis:
- The regex matching QDP commands is not case-insensitive. Matching uses patterns like r"^READ\s+..." without re.IGNORECASE.

Priority: low-medium (parsing bug, small fix expected)

Plan:
1. Make the QDP command regex matching case-insensitive, or normalize lines to upper-case before matching (prefer regex flag re.IGNORECASE to preserve original values).
2. Run the test suite subset for qdp to ensure all tests pass.
3. Create minimal patch modifying only the ascii.qdp reader.
4. Submit patch for review, then hand off to CodeReviewer and then QA.

Deliverables:
- Small PR/patch changing regex matching to be case-insensitive
- Updated tests if needed (but per instructions, do not modify tests)

Notes:
- The reporter attached a qdp.patch that likely uses str.upper() on lines; prefer using re.IGNORECASE on compiled regexes.
- Ensure that numeric parsing isn't affected.

Assignees: Engineer -> CodeReviewer -> QA

Tickets to create:
- EN-0001: Implement case-insensitive QDP command matching
- CR-0001: Code review for the QDP case-insensitivity fix
- QA-0001: Validate QDP parsing for mixed-case commands
