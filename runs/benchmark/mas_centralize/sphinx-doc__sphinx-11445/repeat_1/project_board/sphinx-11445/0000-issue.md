Title: Using rst_prolog removes top level headings containing a domain directive

Repository: sphinx-doc/sphinx
Issue: Using rst_prolog removes top level headings containing a domain directive

Problem summary:
If rst_prolog is set, documents whose top-level heading is a domain role (e.g. :mod:`mypackage`) are not rendered correctly and are omitted from the toctree. The prolog is prepended directly to the RST content without ensuring separation from a section title line, causing the title underline to be associated incorrectly.

Goal:
Produce a minimal fix so that rst_prolog insertion does not break headings that use roles or inline markup at the top of the document. Add tests covering the scenarios with and without trailing newline in prolog.

Failure tests:
- tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_with_newline
- tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_without_newline

Passing tests (relevant):
- tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections

Notes:
The rst_prolog is currently inserted without checking that a blank line exists between the prolog and the document, which can cause the first line (a role inline) to join with the underline marker. The hint suggests ensuring an empty line is added when needed.

Plan:
- Create a small change in sphinx/util/rst.py to ensure a newline is present between prolog and content when inserting prolog. Prefer to only add a single newline (or CRLF handling) to minimize change surface.
- Run tests and iterate until failing tests pass.

Next steps:
- Create an engineer ticket to implement the change.
- After patch is produced, route to CodeReviewer then QA following the SWE-bench workflow.
