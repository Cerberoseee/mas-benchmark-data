Issue: Support header_rows in RestructuredText (RST) writer

Description:
The RST writer (astropy.io.ascii.rst) currently does not accept the "header_rows" parameter
when writing tables, causing a TypeError. Other ASCII writers like fixed_width support header_rows
which allow writing multiple header rows (e.g., column names + units). We need to add support
for header_rows in the RST writer so that QTable.write(format='ascii.rst', header_rows=[...])
works similarly to other writers.

Failing test: astropy/io/ascii/tests/test_rst.py::test_rst_with_header_rows

Goal: Minimal change to support header_rows parameter in RST writer and pass the failing test.

Planned tasks:
- T1: Reproduce failure and run tests locally (Engineer)
- T2: Update RST writer to accept header_rows argument and handle multiple header rows (Engineer)
- T3: Add/adjust unit rendering to include in header rows (Engineer)
- T4: Run test suite for ascii.rst tests (Engineer)
- T5: Code review (CodeReviewer)
- T6: QA run and verification (QA)

Notes:
- Keep changes minimal and confined to astropy/io/ascii/rst.py or related writer factory code.
- Ensure no tests unrelated to RST are broken.
