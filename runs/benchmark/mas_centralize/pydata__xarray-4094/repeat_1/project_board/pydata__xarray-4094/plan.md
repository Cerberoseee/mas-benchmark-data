Plan

1. Engineer: Run the failing test and reproduce. Inspect DataArray.to_unstacked_dataset and Dataset.to_stacked_array implementations to find the MergeError cause. Minimal fix likely in how variables are combined when unstacking single-dim variables; perhaps DataArray.to_unstacked_dataset should treat 1-D variables differently (avoid creating a variable named after the stacked dim 'y' in both datasets causing conflict).

2. Engineer: Implement the fix and run tests.

3. CodeReviewer: Review the patch.

4. QA: Run tests and provide QA_VERDICT.

5. If QA VERIFIED, ProjectManager confirms read_patch_diff shows non-empty patch, then declare PROJECT COMPLETE.

Routing:
- transfer_to_engineer
