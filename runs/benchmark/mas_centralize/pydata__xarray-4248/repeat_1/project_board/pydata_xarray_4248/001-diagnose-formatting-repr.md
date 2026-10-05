Title: Diagnose failing formatting repr test

Objective:
Find the code responsible for formatting Dataset and inline variable reprs, reproduce failing test xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr, and produce a minimal patch suggestion.

Steps for Engineer:
1) Run pytest -k test_inline_variable_array_repr_custom_repr to reproduce locally.
2) Inspect xarray/core/formatting.py and xarray/core/format.py (or similarly named files) to locate functions that produce DataArray/Dataset repr: look for _repr_, _repr_html_, format_items, array_repr, diff_*_repr functions.
3) Add logging/print to confirm which branch is hit when array objects provide custom _repr_short_ or when attrs['units'] exist.
4) Identify where to inject units into the printed line for coords/data variables. Candidate functions: format_items or array header formatting in dataset_repr.
5) Report back with exact function names and suggested minimal code change (helper to extract units and include as part of name string). Include note if other tests need updates.

Success criteria:
- Exact file(s) and function(s) identified with proposed change points.
- Repro steps and failing output captured.
