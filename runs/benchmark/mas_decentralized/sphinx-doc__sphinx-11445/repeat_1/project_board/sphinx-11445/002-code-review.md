Title: Code review: ensure prepend_prolog adds blank line separation correctly

Description

Review the patch that modifies sphinx.util.rst.prepend_prolog. Verify:

- The change is minimal and well-targeted.
- CRLF behavior is preserved (tests for CRLF still pass).
- No other tests are regressed (particularly epilog/append behavior).
- Edge cases: empty prolog, prolog ending with newline, source starting with newline, source using CRLF, prolog with multiple lines.

If acceptable, mark review as approved and transfer to QA.

Assignee: CodeReviewer
