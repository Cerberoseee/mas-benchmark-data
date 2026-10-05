Title: --notes option ignores note tags that are entirely punctuation

Repository: pylint-dev/pylint
Issue ID: 5859 (from SWE-bench instance)

Summary:
When using the --notes CLI option to specify note tags (fixme tags), tags that are composed solely of punctuation (e.g., "???") are ignored and do not trigger W0511 fixme warnings. The implementation treats --notes as a regex and does not escape special regex characters, so tokens like "?" are interpreted as regex metacharacters.

Reproduction:
- Create test.py containing:
  # YES: yes
  # ???: no
- Run: pylint test.py --notes="YES,???"
- Only the YES line is reported; ??? is ignored.

Root cause hypothesis:
The code converts the comma-separated list from --notes into a regex without escaping user-provided literal tokens, so punctuation-only tokens like "???" are malformed regexes (interpreted with special meaning) and don't match the literal tag.

Scope and constraints:
- Minimize code changes; prefer escaping the tokens provided via --notes to treat them as literals or otherwise ensure behavior matches notes-rgx semantics.
- Tests to adjust: the failing test is tests/checkers/unittest_misc.py::TestFixme::test_non_alphanumeric_codetag

Plan:
1. Create a small code change in the parser or the part that constructs the notes regex from --notes to escape tokens properly (e.g., re.escape on each token).
2. Run unit tests for fixme-related tests.
3. If tests pass, create PR/patch and request QA.

Deliverables:
- Patch implementing escaping of --notes tokens.
- Update/ensure tests pass (the harness applied gold test changes already).

Assignments:
- Engineer: implement the escaping and run tests.
- QA: run the failing test and provide QA_VERDICT with verified: true/false and failing_ids if any.

Notes:
- Constrain changes to minimize risk; do not touch notes-rgx option behavior.
- Confirm that the patch diff is non-empty before declaring completion.