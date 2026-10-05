Title: Implement header_rows support in RST writer

Description:
The RST writer class currently does not accept the optional header_rows
parameter. Modify the RST writer to accept header_rows and render additional
header rows (such as units) similar to fixed_width writer behavior.

Acceptance criteria:
- RST writer __init__ accepts header_rows kwarg.
- Writing a table with header_rows produces output that includes the extra
  header rows between the border and the data rows, and aligns columns
  appropriately.
- Existing rst read/write tests continue to pass.

Notes:
- Focus on minimal changes—do not refactor unrelated parts.
- See astropy/io/ascii/writetbl.py (or relevant module) for patterns.

Files likely to change:
- astropy/io/ascii/rst.py or astropy/io/ascii/core.py (where RST writer is defined)
- Possibly tests are already provided.

Estimate: 1-2 hours
Assignee: Engineer
