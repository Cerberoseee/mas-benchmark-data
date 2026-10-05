Title: Triage for astropy issue: Possible bug in io.fits related to D exponents

Summary:
User reports that in fitsrec.py there is code that attempts to replace exponent separator in floating point numbers:

    # Replace exponent separator in floating point numbers
    if 'D' in format:
        output_field.replace(encode_ascii('E'), encode_ascii('D'))

They believe replace on numpy.chararray is not in-place and thus the code has no effect. Tests fail for ascii table checksum and ascii table reading. Changing to use the returned value may be necessary. Commenting out the code doesn't cause tests to fail locally for them, but CI shows two failing tests in our harness.

Files of interest:
- astropy/io/fits/fitsrec.py
- astropy/io/fits/tests/test_checksum.py::TestChecksumFunctions::test_ascii_table_data
- astropy/io/fits/tests/test_table.py::TestTableFunctions::test_ascii_table

Impact:
- Potential incorrect formatting of ASCII table floating point exponents when 'D' is expected; could result in wrong checksum or table parsing.
- Tests failing in our suite indicate a bug or mismatch with expected behavior.

Proposed next steps (tickets):
1) Create a small diagnostic ticket to reproduce and add focused tests to assert behavior of replacing 'E' with 'D' in fitsrec for ascii tables.
2) Implement minimal fix in fitsrec.py to use the result of replace (assign back to output_field) or use numpy.char.replace which returns a new array; ensure no in-place expectation.
3) Run unit tests that failed and adjacent tests to ensure no regressions.
4) Code review and QA validation.

I'll create these tickets and route to Engineer for implementation.
