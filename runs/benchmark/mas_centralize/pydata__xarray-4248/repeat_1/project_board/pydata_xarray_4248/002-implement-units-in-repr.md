Title: Implement units display in repr for Dataset/DataArray

Objective:
Modify formatting code to include units for coordinates and data variables when available. Extract units from attrs['units'] and from unit-aware arrays when possible.

Acceptance criteria:
- The failing test xarray/tests/test_formatting.py::test_inline_variable_array_repr_custom_repr passes.
- No regressions in other formatting tests.
- Patch is minimal and constrained to formatting module(s).

Implementation guidance:
- Add helper function get_unit(obj) in xarray/core/formatting.py (or wherever formatting helpers live).
  - Priority: if obj is a DataArray or Variable with attrs.get('units'), return that string.
  - Else if obj has attribute 'unit' or 'units', return str(obj.unit) or str(obj.units). Support pint.Quantity's .units property.
  - Else, if obj implements NEP-18 _repr_short_ and its repr includes unit in a standardized form, try to parse? Better to avoid parsing; prefer direct attribute checks.
- Modify the code that builds the per-variable line (both coordinates and data variables) to append ' [units]' or ', in {units}' as per chosen formatting. Keep formatting conservative: use square brackets after the name: 'name [unit]'. Example: 'rainfall [mm]  (time, y, x) float32 ...'
- Ensure alignment still reasonable; reuse existing alignment logic where possible.
- Add/adjust tests as necessary only if harness applies gold patch.

Notes:
- Avoid heavy coupling to any particular units library. Use duck-typing for .units/.unit attributes.
- If encountering array-like objects that embed units in repr, don't special-case parsing unless necessary for tests.
