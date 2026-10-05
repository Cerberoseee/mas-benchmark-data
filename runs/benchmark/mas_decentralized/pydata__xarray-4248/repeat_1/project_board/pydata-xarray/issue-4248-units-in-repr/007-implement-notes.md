Implemented honoring NEP-18 _repr_inline_ method for duck arrays in xarray.core.formatting.inline_variable_array_repr.

- Updated inline_variable_array_repr to call _repr_inline_ if present on the underlying data.
- Falls back to existing behavior on exceptions or if None is returned.
- Added small try/except to be defensive.

Tests run: targeted failing test and related formatting tests passed locally.
