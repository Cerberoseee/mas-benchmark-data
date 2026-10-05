QA smoke-test output and QA_VERDICT

Smoke-test run (by QA):
- Command: python3 scripts/tests/media_merge_smoketest.py
- Output:
  INPUT: [['a.js', 'b.js', 'c.js'], ['b.js', 'd.js'], ['c.js', 'e.js']]
  MERGED: ['a.js', 'b.js', 'c.js', 'd.js', 'e.js']
  ----------------------------------------
  INPUT: [None, ['a.js', 'b.js'], None, ['b.js', 'c.js']]
  MERGED: ['a.js', 'b.js', 'c.js']
  ----------------------------------------
  INPUT: []
  MERGED: []
  ----------------------------------------
- Exit code: 0

QA_VERDICT:
  verified: false
  failing_ids:
    - test_combine_media (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_construction (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_form_media (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_media_deduplication (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_media_inheritance (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_media_inheritance_extends (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_media_property_parent_references (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_merge (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_merge_css_three_way (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_merge_js_three_way (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_merge_js_three_way2 (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_merge_warning (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_multi_widget (forms_tests.tests.test_media.FormsMediaTestCase): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_media (admin_widgets.test_autocomplete_widget.AutocompleteMixinTests): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_render_options (admin_widgets.test_autocomplete_widget.AutocompleteMixinTests): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted
    - test_inline_media_only_inline (admin_inlines.tests.TestInlineMedia): test collection blocked — pytest not available to workspace Python and pytest binary execution is not allowlisted

QA notes:
- The smoke-test demonstrates the heuristic merging behavior but does not guarantee full test-suite compatibility. Full verification requires pytest availability.
- QA awaits either the exact reproducer output for the ticket example (text-editor.js case) or pytest-based test runs.
