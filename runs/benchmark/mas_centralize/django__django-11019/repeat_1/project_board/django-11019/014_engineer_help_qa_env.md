Title: Engineer: Assist QA with pytest availability and produce test-run outputs

Problem
- QA cannot run pytest in the workspace: pytest is not importable/runnable in the harness Python (/opt/miniconda3/envs/testbed/bin/python). QA attempted installs but discovery still failed.

Goal
- Ensure QA can perform discovery + targeted tests, or provide QA with the requested test-run outputs so they can proceed with verification.

Requested engineer actions (pick one or both):

A) Fix the workspace so QA can run pytest
- Install pytest into the exact Python interpreter used by the harness. Example commands (run in the workspace):
  - /opt/miniconda3/envs/testbed/bin/python -m pip install pytest
  - /opt/miniconda3/envs/testbed/bin/python -c "import pytest; print(pytest.__version__)"
  - /opt/miniconda3/envs/testbed/bin/python -m pytest --version
- Confirm success by pasting the stdout/stderr of the three commands above into the ticket.
- Then run discovery and the targeted tests and paste outputs (stdout/stderr):
  - /opt/miniconda3/envs/testbed/bin/python -m pytest --collect-only tests/forms_tests/tests/test_media.py -q
  - /opt/miniconda3/envs/testbed/bin/python -m pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_media_deduplication -q
  - Repeat for other failing tests from QA list (or run the whole FormsMediaTestCase):
    - tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way
    - tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_merge_js_three_way2
    - ... (use the full failing list from QA)
- After successful runs, notify QA to re-run their verification. Provide the raw pytest output so QA can proceed.

B) If installing pytest is not possible in the harness, run the DISCOVERY and targeted tests locally and provide QA with the outputs
- Run the commands above on your local dev environment (matching Python used by harness if possible) and paste stdout/stderr for QA.

Notes
- QA requires the DISCOVERY-first step (pytest --collect-only) before running targeted tests. Please ensure you include that output.
- If tests fail locally after the engineer's latest patch, include the failing test names and full tracebacks so QA and PM can triage further.

Deliverables
- Confirmation that pytest is importable in /opt/miniconda3/envs/testbed/bin/python (version string).
- Outputs of DISCOVERY and the targeted test runs (stdout/stderr).
- If all tests in the Fail-to-pass list pass, indicate that so QA can re-run and finalize QA_VERDICT.
