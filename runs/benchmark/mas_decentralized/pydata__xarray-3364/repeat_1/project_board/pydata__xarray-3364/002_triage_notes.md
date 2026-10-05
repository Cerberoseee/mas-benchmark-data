Triage notes:

Initial failing tests show concat and auto-combine expect all datasets to have same variables. Desired behavior is to union variables and fill missing with NaN. Location to inspect: xarray/core/combine.py and xarray/core/concat.py. Potential helper functions: Dataset.reindex or Dataset.align may help; also xarray.combine_by_coords implementation.

Plan: Engineer will implement in concat path: compute union of variable names, for each dataset missing a variable, create DataArray of appropriate shape filled with NaN and same coords/dims as expected, then proceed with existing concat logic. For auto-combine, ensure the function that merges datasets uses outer join for variables.
