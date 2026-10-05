Status: completed

I implemented a minimal fix in pylint/checkers/misc.py so that notes supplied via --notes are matched even when they are entirely punctuation. The regex now uses a lookahead (?=(?:\b|:|\s|$)) instead of a trailing word boundary, which made punctuation-only tags like ??? fail to match. All targeted tests pass.

Changed file:
- pylint/checkers/misc.py

Tests run:
- tests/checkers/unittest_misc.py::TestFixme::test_non_alphanumeric_codetag (now passes)
- plus the listed pass-to-pass tests (all pass)

Commit: fix: handle non-alphanumeric note tags in fixme detection by using lookahead boundary (allow punctuation-only tags)
