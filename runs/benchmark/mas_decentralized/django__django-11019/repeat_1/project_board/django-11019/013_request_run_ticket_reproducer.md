Request to Engineer: add exact ticket reproducer and provide run outputs

Background:
- QA ran the smoke-test and confirmed the heuristic merge behavior, but could not run pytest in this workspace.
- QA needs the exact ticket reproducer (ColorPicker/SimpleTextWidget/FancyTextWidget/MyForm) run via the smoke-test so they can validate the specific example without pytest.

Please do these exact steps and commit the changes:

1) Update scripts/tests/media_merge_smoketest.py to include the exact ticket example from the issue:
   - Create Media objects as in the ticket:
     - ColorPicker: js = ['color-picker.js']
     - SimpleTextWidget: js = ['text-editor.js']
     - FancyTextWidget: js = ['text-editor.js', 'text-editor-extras.js', 'color-picker.js']
   - Build the final merged Media for the form (simulate MyForm media) and print both the merged result and the expected result.
   - Expected merged order for the example: ['text-editor.js', 'text-editor-extras.js', 'color-picker.js']

2) Run the smoke-test in the workspace Python and capture stdout/stderr and exit code. Paste the output into the project board under data/project_board/django-11019/014_engineer_ticket_reproducer_output.md

3) If you can run pytest locally (outside this workspace), run and paste outputs for the following commands (stdout/stderr and return codes):
   - pytest --maxfail=1 --disable-warnings --collect-only tests/forms_tests/tests/test_media.py
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way -q
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way2 -q
   - pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge -q

   If tests fail, include tracebacks and update the implementation accordingly.

4) Commit the changes and then transfer to CodeReviewer for quick review, then to QA for re-run. If you cannot run pytest locally, at minimum provide the smoke-test output including the ticket reproducer.

Notes:
- This is necessary because the workspace does not allow running pytest currently. QA has confirmed the heuristic script runs; the ticket example must be demonstrated to proceed.

Deliverables (must be posted to project_board):
- scripts/tests/media_merge_smoketest.py (updated)
- data/project_board/django-11019/014_engineer_ticket_reproducer_output.md (smoke-test stdout/stderr)
- Optional: local pytest outputs (if available)

Assigned to: Engineer
