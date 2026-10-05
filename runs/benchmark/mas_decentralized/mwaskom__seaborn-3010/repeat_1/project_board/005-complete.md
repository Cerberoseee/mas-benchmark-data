T-PolyFit-001: Fix PolyFit to handle missing data

Status: Completed

Notes:
- Dropped rows with NA in x or y before calling np.polyfit
- Added guard for insufficient unique x values
- Tests updated: all target tests pass locally
