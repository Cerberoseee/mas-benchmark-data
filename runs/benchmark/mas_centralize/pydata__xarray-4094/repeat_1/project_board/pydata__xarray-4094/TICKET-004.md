TICKET-004: QA validation

Description:
- Run the full test suite subset (at least xarray/tests/test_dataset.py::TestDataset::test_to_stacked_array_to_unstacked_dataset and nearby tests) after the patch is applied.
- Provide QA_VERDICT block indicating verified: true/false and failing_ids with notes.

Acceptance criteria:
- Confirm failing test passes and no new failures introduced.

Assignee: QA