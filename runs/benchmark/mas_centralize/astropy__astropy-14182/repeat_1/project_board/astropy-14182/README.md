Issue: Support header_rows in RestructuredText (rst) writer for Table

Repository: astropy/astropy
Issue summary:
The RST writer (io.ascii.rst) does not accept header_rows parameter, causing
TypeError when writing tables with header_rows (like units + names rows). This
prevents writing QTable with header rows into rst format.

Goal: Add support for header_rows to RST writer with minimal changes so that
astropy/io/ascii/tests/test_rst.py::test_rst_with_header_rows passes.

Approach:
- Inspect rst writer class and its init signature; accept header_rows kwarg.
- Reuse existing handling in fixed_width writer for header_rows behavior.
- Add/adjust tests if needed but harness already has failing test.

Work items:
- Engineer: Implement minimal change to accept header_rows and render them in rst output.
- Code review: Quick scope/safety check of diff.
- QA: Run tests and verify failing test now passes.

Workflow: Engineer -> CodeReviewer -> QA -> ProjectManager
