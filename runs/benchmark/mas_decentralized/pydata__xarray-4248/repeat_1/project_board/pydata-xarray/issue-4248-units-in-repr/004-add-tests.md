Engineer ticket 004-add-tests

Goal: Add or adjust tests to cover units shown in reprs. Focus on minimal changes to satisfy failing test:
- Reproduce failing test xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr and ensure custom repr unaffected.
- Add new tests to assert unit string inclusion when attrs['units'] present and when array is pint.Quantity-like (if detection present).

Deliverables:
- Test(s) in xarray/tests/test_formatting.py or new tests file.

Estimate: 2h.

Assignee: Engineer
Labels: tests