Title: Ensure rst_prolog is separated from document content by a newline when necessary

Assignee: Engineer
Type: task

Description:
Modify sphinx/util/rst.py to ensure that when rst_prolog is prepended to the source RST content, there is at least one newline separating the prolog from the document. Handle CR, CRLF, and LF line endings appropriately and avoid changing content if already separated.

Acceptance criteria:
- Existing tests remain passing, and the two failing tests in tests/test_util_rst.py (test_prepend_prolog_with_roles_in_sections_with_newline and test_prepend_prolog_with_roles_in_sections_without_newline) pass.
- The change is minimal and only touches sphinx/util/rst.py.
- Include a small comment explaining why the newline is added.

Implementation hints:
Look at the current prepending logic in sphinx/util/rst.py lines ~81-91. Add logic that checks whether the prolog ends with a newline and whether the source begins with a title line that could be merged with a following underline. Simplest approach: ensure prolog ends with a newline and source begins with a newline; if not, insert a single configurable newline between them.

Run tests:
pytest tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_with_newline -q
pytest tests/test_util_rst.py::test_prepend_prolog_with_roles_in_sections_without_newline -q

Deliverables:
- Patch committed to repo. Ensure to run read_patch_diff and attach the diff to the ticket when done.
