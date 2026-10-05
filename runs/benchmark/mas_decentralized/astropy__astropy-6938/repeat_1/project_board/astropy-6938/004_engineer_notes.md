Triage: Investigated potential bug in fitsrec.py where chararray.replace() call was used without assigning the result. Reproduced failing tests for ASCII table checksum and ascii table writing. Fix: assign the result of output_field.replace(...) back into output_field via output_field[:] = ... to perform in-place modification of array contents. Committed change. Verified targeted tests pass.

Changed file:
- astropy/io/fits/fitsrec.py

Notes:
- The original code called output_field.replace(...), which for numpy.chararray returns a new array and does not modify in place. This caused written ASCII table data to keep E exponents rather than D, altering checksum values.
- The fix preserves behaviour (use D in format) but ensures the replacement actually takes effect.

Status: Ready for Code Review and QA.