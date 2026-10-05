Code review notes:
- Modified xarray/core/concat.py to collect only existing variables when merging variables_to_merge.
- Ensures missing variables do not cause a ValueError; merging uses available variables.
- Added sanity check to ensure variable appears at least once.
