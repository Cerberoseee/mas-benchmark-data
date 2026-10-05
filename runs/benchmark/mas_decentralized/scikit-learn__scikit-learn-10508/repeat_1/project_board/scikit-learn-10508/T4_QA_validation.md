Title: T4 - QA validation: run label tests

Description:
Run the label-related tests and confirm the bug is fixed. Provide a
QA_VERDICT block with verified:true/false and failing_ids if any.

Tasks:
- Execute pytest on sklearn/preprocessing/tests/test_label.py::test_label_encoder_empty_array
  and related label tests listed in the issue.
- If failures, capture pytest output and failing test ids.

Assignee: QA.