Status: implemented

Summary:
- Fixed bug: rst_prolog insertion broke top-level headings starting with role directives (e.g. :mod:`...`).
- Root cause: docinfo regex matched role-like lines and treated them as docinfo; prolog insertion then disturbed section parsing.

Files changed:
- sphinx/util/rst.py

Commit: d73f7999fd62b4cd3817602064ad820c767ed8c7

Validation:
- Ran targeted tests: tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_with_newline (passed)
- Ran targeted tests: tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_without_newline (passed)
- Related tests in tests/test_util_rst.py all passed.

Notes for reviewer/QA:
- The change modifies the docinfo_re to avoid matching role-like constructs at the start of a line. Please review the regex and consider additional role patterns if needed.
