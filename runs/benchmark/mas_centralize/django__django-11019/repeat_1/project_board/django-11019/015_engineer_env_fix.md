Title: Engineer: Resolve QA environment blockage (pytest not importable) and provide test-run outputs

Context
- QA attempted to run discovery and targeted tests to verify the Media.merge fix but could not because pytest is not importable/runnable in the workspace Python.
- QA returned QA_VERDICT: verified: false due to test collection failure. The failing_ids list is a result of that collection failure (pytest not present).

Required actions (pick one):

Option A — Fix workspace so QA can run tests
1. Install pytest into the exact Python interpreter used by the QA harness. Example (run in the workspace):
   - /opt/miniconda3/envs/testbed/bin/python -m pip install pytest
   - /opt/miniconda3/envs/testbed/bin/python -c "import pytest; print(pytest.__version__)"
   - /opt/miniconda3/envs/testbed/bin/python -m pytest --version
2. Provide the stdout/stderr outputs of the three commands above in a reply on the project board.
3. Run DISCOVERY and the targeted tests and paste outputs (stdout/stderr) for QA to consume:
   - /opt/miniconda3/envs/testbed/bin/python -m pytest --collect-only tests/forms_tests/tests/test_media.py -q
   - /opt/miniconda3/envs/testbed/bin/python -m pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_media_deduplication -q
   - /opt/miniconda3/envs/testbed/bin/python -m pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way -q
   - (repeat for the rest of the QA failing_ids or run the whole FormsMediaTestCase)
4. Notify QA to re-run their verification. QA will return a QA_VERDICT block (verified: true/false).

Option B — If workspace changes are not permissible
1. Run the DISCOVERY and the same targeted tests locally in an environment matching the harness's Python version.
2. Capture and paste the raw pytest outputs (collect-only and test runs) to the project board so QA can review.
3. QA will review logs and produce a QA_VERDICT accordingly.

QA_VERDICT excerpt (from last run)
- verified: false
- failing_ids (collection aborted due to missing pytest):
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

Notes
- The engineer's patch is already committed (non-empty). QA needs working pytest in the harness to validate. This is an environment/platform issue rather than a code issue.
- If you need to run the tests locally and cannot install pytest on the harness, please follow Option B and provide the raw outputs.

Once QA returns verified: true and I (PM) confirm the patch is non-empty, I will mark PROJECT COMPLETE.
