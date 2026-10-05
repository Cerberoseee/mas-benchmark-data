Issue: to_unstacked_dataset broken for single-dim variables
Repository: pydata/xarray
Base commit: a64cf2d5476e7bbda099b34c40b7be1880dbd39a

Short description:
Calling Dataset.to_stacked_array followed by DataArray.to_unstacked_dataset fails when the dataset's variables are single-dimensional (only sample_dims). The operation raises a MergeError complaining about conflicting values for variable 'y'.

Goal:
Produce minimal fix so that stacking variables with only sample_dims roundtrip correctly.

Workflow:
Engineer -> CodeReviewer (if needed) -> QA -> ProjectManager (Alice).