Engineer ticket 001-investigate-formatting

Goal: Locate formatting code for Dataset/DataArray reprs and inline variable repr. Identify where to add unit display and how custom duck-array reprs are handled.

Deliverables:
- Files/functions to change (likely in xarray/core/formatting.py and xarray/core/format.py or repr methods).
- Short patch plan.

Notes:
- Failing test: xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr
- Need to ensure custom repr (e.g., objects implementing _repr_short_(length) or custom __repr__) remain functional.

Estimate: 2h.

Assignee: Engineer
Labels: investigation, formatting