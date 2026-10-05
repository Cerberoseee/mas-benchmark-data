Action required from Engineer: Add exact ticket reproducer + local pytest outputs

Context:
- QA is blocked from running pytest in the workspace (pytest not importable / pytest binary not allowlisted). QA did run the smoke-test script and confirmed the heuristic behavior, but could not run the project's pytest-based tests.

Please do the following (small, targeted steps):

1) Extend the smoke-test script to include the exact ticket example (ColorPicker / SimpleTextWidget / FancyTextWidget / MyForm) so QA can validate the desired outcome without pytest. Add a function that creates widget Media objects the same way as in the ticket, constructs the final form-level Media (or builds and sets m._js_lists appropriately), and prints both the merged result and the expected result.

   - Desired expected merged JS order for the example: ['text-editor.js', 'text-editor-extras.js', 'color-picker.js']
   - Place the new code in scripts/tests/media_merge_smoketest.py and commit.

2) Run the smoke-test in the workspace Python and paste stdout/stderr here (or add the output to the project board as a new file). This will allow QA to re-run the smoke-test and verify the ticket example.

3) If you can run pytest locally (outside the blocked workspace), run these commands and paste their outputs here (stdout/stderr and return codes):
   - pytest --maxfail=1 --disable-warnings --collect-only tests/forms_tests/tests/test_media.py
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way -q
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way2 -q
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way (and any other failing IDs from QA_VERDICT)

   If any tests fail, provide the failing tracebacks and adjust the patch accordingly.

4) If you cannot run pytest locally, add more smoke-test cases that reproduce the failing tests from QA_VERDICT (e.g., the ones in test_media that the ticket referenced) to demonstrate behavior.

Deliverables:
- Updated scripts/tests/media_merge_smoketest.py containing the exact ticket reproducer and sample cases.
- Smoke-test run output (stdout/stderr) saved to project_board (or pasted here).
- If available, pytest collection / targeted test run outputs saved to project_board (or pasted here).

Why this is needed:
- QA cannot run pytest in this workspace; adding the precise reproducer and outputs lets QA validate the specific behavior and assess whether the heuristic fix actually resolves the ticket example.

Please make the changes, commit them, and then transfer back to QA. If you push changes, also transfer to CodeReviewer for quick review before QA re-run.

Assigned to: Engineer
