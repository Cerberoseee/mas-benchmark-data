Title: io.fits possible bug: non-inplace replace of exponent separator

Repo: astropy/astropy
Issue: Possible bug in io.fits related to D exponents in fitsrec.py — `chararray.replace` used as if in-place

Description:
User reports code in astropy/io/fits/fitsrec.py:

```
        # Replace exponent separator in floating point numbers
        if 'D' in format:
            output_field.replace(encode_ascii('E'), encode_ascii('D'))
```

This likely expects replace to mutate the chararray in-place, but numpy.char.replace returns a new array, so this probably is a no-op as written. Tests that exercise this behavior don't fail, suggesting either code path not covered or behavior doesn't matter because FITS treats D/E the same in reading.

Failing tests (from harness):
- astropy/io/fits/tests/test_checksum.py::TestChecksumFunctions::test_ascii_table_data
- astropy/io/fits/tests/test_table.py::TestTableFunctions::test_ascii_table

Goal: Fix the in-place replacement so that exponent separators 'E' -> 'D' are actually replaced in output_field, with minimal change surface.

Constraints/Notes:
- Avoid broad redesign; prefer minimal, well-scoped change.
- Tests already included by harness (gold patch) should not be edited.
- Implementer must ensure non-empty patch and follow handoffs to QA.

Plan (high-level):
1. Reproduce failing tests locally in CI harness.
2. Inspect fitsrec.py and related code to understand types of `output_field` (numpy.chararray?) and ensure proper replace semantics.
3. Apply small patch to assign the replaced array back to output_field (or use numpy.char.replace) so replacement is effective.
4. Run tests; if failing, iterate.
5. Once passing, create PR-style patch and hand off to QA.

Deliverables:
- Patch that ensures 'D' exponent replacement actually occurs.
- Project board tickets for implementation, review, QA, and handoffs.
