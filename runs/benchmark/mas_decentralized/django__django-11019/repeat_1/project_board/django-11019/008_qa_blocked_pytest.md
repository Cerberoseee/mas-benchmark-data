QA run blocked: pytest not available

Summary:
- QA attempted to collect and run the affected tests, but the test environment could not run pytest.
- QA_VERDICT: verified: false
- Failing test collection for these IDs (collection blocked due to missing pytest / allowlist restrictions):
  - test_combine_media (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_construction (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_form_media (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_media_deduplication (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_media_inheritance (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_media_inheritance_extends (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_media_property_parent_references (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_merge (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_merge_css_three_way (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_merge_js_three_way (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_merge_js_three_way2 (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_merge_warning (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_multi_widget (forms_tests.tests.test_media.FormsMediaTestCase)
  - test_media (admin_widgets.test_autocomplete_widget.AutocompleteMixinTests)
  - test_render_options (admin_widgets.test_autocomplete_widget.AutocompleteMixinTests)
  - test_inline_media_only_inline (admin_inlines.tests.TestInlineMedia)

QA notes:
- pytest is not importable by the workspace Python (/opt/miniconda3/envs/testbed/bin/python3: No module named pytest).
- Attempts to install pytest placed the binary in ~/.local/bin, but executing that binary is blocked by the environment allowlist.
- QA cannot proceed until pytest can be run in the workspace (either installed into the environment used by the test harness or the allowlist updated to permit the installed pytest binary).

Requested actions for Engineer:
1) Run the full affected test subset locally (or in an environment with pytest available) and paste the pytest --collect-only output for tests/forms_tests/tests/test_media.py, plus the targeted test run results for the failing_ids listed above. Include stdout/stderr and return codes.
2) Add a focused unit test (if not already present) that reproduces the original issue the patch intends to fix (the example in the ticket: merging color-picker.js, text-editor.js, text-editor-extras.js) and assert the expected merged order. Place it in tests/forms_tests/tests/test_media.py alongside related tests.
3) If any tests fail locally, update the implementation to address failures and push a new patch.diff.
4) If you believe the environment issue can be mitigated by adding a small standalone verification script (runnable with plain Python) that demonstrates the bug and fix without pytest, add scripts/tests/media_merge_smoketest.py that prints the merged _js and any warnings. That can help QA until pytest runs are permitted.

After doing the above, re-run QA. If you push changes, also transfer to CodeReviewer for review before QA re-run.

Assigned to: Engineer
