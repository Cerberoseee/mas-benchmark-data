Title: Fix: Ensure exponent replacement uses non-inplace numpy.chararray.replace result

Goal:
Fix a bug in astropy/io/fits/fitsrec.py where code calls output_field.replace(encode_ascii('E'), encode_ascii('D')) but does not use the returned value. numpy.chararray.replace is not in-place; the call must assign the result back to output_field (or use numpy.char.replace). This causes incorrect ASCII table exponent formatting and failing tests.

Acceptance criteria:
- Update fitsrec.py so that when 'D' in format, the replacement is assigned back to output_field.
- All previously failing tests in the suite now pass.
- Keep changes minimal and localized.

Implementation notes:
- Locate the block in fitsrec.py and change to:
    if 'D' in format:
        output_field = output_field.replace(encode_ascii('E'), encode_ascii('D'))

- Run targeted pytest for the two failing tests and related checksum/table tests.

Risks:
- Minimal. Ensure no other code depends on replace being in-place.

Estimate: 1-2 hours.

Assigned to: Engineer
