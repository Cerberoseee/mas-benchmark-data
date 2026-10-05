- T-astropy-6938: Fixed D exponent replacement in fitsrec.py
  * Modified astropy/io/fits/fitsrec.py to assign the result of chararray.replace back into the array so the replacement is applied in-place.
  * Ran targeted failing tests (astropy/io/fits/tests/test_checksum.py::TestChecksumFunctions::test_ascii_table_data and astropy/io/fits/tests/test_table.py::TestTableFunctions::test_ascii_table) and they now pass.
  * Committed change: "fix(fits): ensure D exponent replacement is applied in-place"
