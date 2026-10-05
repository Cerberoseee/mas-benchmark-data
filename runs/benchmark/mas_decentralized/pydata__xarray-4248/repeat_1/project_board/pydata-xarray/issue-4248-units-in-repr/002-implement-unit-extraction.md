Engineer ticket 002-implement-unit-extraction

Goal: Implement a small helper function in xarray.core.formatting (or utils) to extract a unit string for a variable or array. Behavior:
- If object has attrs and attrs.get('units') -> return that string (trimmed).
- Else, if object is pint.Quantity-like: try to import pint and detect quantity via duck-typing (has attribute 'units' or 'magnitude' or 'units' str). If pint is not installed or detection fails, return None.
- Else, if object defines _repr_short_ or array-style repr, do not attempt to parse units from repr to avoid breaking custom reprs.

Deliverables:
- xarray/core/units.py or integrate into formatting module with tests.

Estimate: 2h.

Assignee: Engineer
Labels: implementation, formatting