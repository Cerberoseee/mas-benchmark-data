Status: implemented

I updated astropy/io/ascii/rst.py to accept header_rows in the RST constructor and to correctly write RST tables when multiple header_rows are present.

Changes:
- RST.__init__ now accepts header_rows and propagates them to header and data, adjusting data.start_line.
- RST.write updated to compose the top border, header rows, separator border, data lines, and bottom border.

I ran the targeted tests: astropy/io/ascii/tests/test_rst.py::test_rst_with_header_rows now passes, and the related read/write tests also pass locally.