Title: Using rst_prolog removes top level headings containing a domain directive

Summary

When rst_prolog is set, a document whose top-level heading is a role/domain directive (e.g. :mod:`name`) loses its heading and it's omitted from the toctree. The repo's rst prolog insertion logic simply concatenates the prolog and source without ensuring a blank line between the prolog and the document content; when the document starts with an interpreted text role or directive and an underline follows, the inserted text can break the section title detection.

Root cause

sphinx.util.rst.prepend_prolog appends prolog directly before the source. If the source begins with a role (`:mod:\`...\``) and immediately follows with an underline (``====``) the combined text may form an interpreted text node connected to the underline, causing the parser to not recognize it as a section title. The fix is to ensure there's at least one blank line separating the prolog and the source when necessary.

Scope

- Failing tests:
  - tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_with_newline
  - tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_without_newline
- Passing tests included several other tests around prolog/epilog handling.

Plan

1. Implement a minimal change in sphinx.util.rst.prepend_prolog to ensure the prolog and source are separated by a blank line when necessary. Prefer appending a single `"\n"` (or `"\r\n"` preservation) rather than large restructuring.
2. Add/adjust unit tests if required (note: harness already applied gold test patch). Run test subset.
3. Submit a focused patch and request CodeReviewer review.
4. After review, hand to QA to run full tests.

Acceptance criteria

- The two failing tests pass.
- No unrelated tests regressed.

Notes

- The hint suggests simply adding an empty line after the prolog internally.
- Keep change minimal to avoid affecting other prolog behavior. Preserve CRLF when source uses CRLF.
