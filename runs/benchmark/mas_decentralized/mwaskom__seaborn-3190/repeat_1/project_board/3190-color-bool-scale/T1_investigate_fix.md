Status: Fixed

Summary:
- Reproduced failing case: color mapping with boolean data raised TypeError in Continuous._setup when computing normalization: forward(vmax) - forward(vmin) failed for boolean arrays.
- Root cause: transform forward() returned boolean or boolean-array; subtracting booleans with numpy triggers a TypeError.
- Fix: coerce transform outputs to float before subtraction and normalization using np.asarray(..., dtype=float).

Changes made:
- Modified seaborn/_core/scales.py to coerce forward(vmin)/forward(vmax) outputs to float when computing normalization for Continuous scales.
- Commit message: fix(scales): coerce boolean transform outputs to float in Continuous normalization

Testing:
- Ran targeted test: tests/_core/test_scales.py::TestContinuous::test_interval_with_bools — now passes.
- Ran full scales tests file tests/_core/test_scales.py — all tests passed (with unrelated runtime warnings).

Next steps:
- Request CodeReview and QA to validate patch and run broader test suite as needed.
