Engineer patch summary:

Commit: 73764a998f9ae3fc344441ecb6fb622e95342010
File changed: xarray/core/formatting.py
Summary of changes:
- Added support for NEP-18 duck arrays by calling _repr_inline_ if available when generating inline variable repr.
- Handles TypeError fallback to maybe_truncate(str(var._data), max_width)

Test run results reported by Engineer:
- After fix, tests: 18 passed, 11 warnings

Next steps (per workflow):
- Code review needed
- QA to run failing test(s) and formatting suite
