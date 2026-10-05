T-000: Fix concat to ignore missing variables when merging.

Action: patched xarray/core/concat.py to collect only present variables when merging instead of raising when some datasets lack them.

Tests run: targeted failing tests for concat and combine. Both now pass locally.
