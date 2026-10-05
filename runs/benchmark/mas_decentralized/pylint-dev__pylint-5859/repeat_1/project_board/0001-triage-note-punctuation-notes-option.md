Title: --notes option ignores note tags that are entirely punctuation

Summary:
If a note tag specified with the --notes option is entirely punctuation (e.g. "???"), pylint won't report W0511 (fixme) for comment lines containing that tag. The option parsing converts the comma-separated list into a regular-expression without escaping special regex characters, so tags containing regex metacharacters are interpreted as regex syntax instead of literals.

Reproduction:
1. Create test.py with:
   # YES: yes
   # ???: no
2. Run: pylint test.py --notes="YES,???"
3. Only the YES line is reported; the ??? line is ignored.

Failing test:
- tests/checkers/unittest_misc.py::TestFixme::test_non_alphanumeric_codetag

Root cause hypothesis:
When building the pattern for notes from the --notes option, tags are embedded into a regex without escaping, so punctuation-only tags like "???" are treated as regex tokens and don't match literally.

Minimal fix:
Escape each tag from the --notes option with re.escape before joining them into a combined regex, preserving the semantics of the notes-rgx option (which intentionally accepts arbitrary regex expressions).

Files likely touched:
- pylint/checkers/misc.py (Fixme checker)
- pylint/checkers/utils or config parsing could be involved but start in misc.py

Acceptance criteria:
- A non-empty patch that escapes tags correctly.
- Tests: the failing test listed above passes, and the other listed pass-to-pass tests still pass.
- Code reviewer approves patch; QA verifies tests.

Estimate: 1-2 engineer days

Assigned: ENGINEER (see handoff)
