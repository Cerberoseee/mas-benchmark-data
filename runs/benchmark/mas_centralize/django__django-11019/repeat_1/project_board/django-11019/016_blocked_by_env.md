Status: BLOCKED — QA cannot run tests due to missing pytest in workspace

Summary:
- Engineer implemented and committed a non-empty patch to django/forms/widgets.py that changes Media merging to a multi-list topological merge. CodeReviewer approved.
- QA attempted verification but could not run pytest (pytest not importable in the harness Python), returned QA_VERDICT: verified: false.

Required actions (choose one):
A) Platform: Install pytest into the exact Python interpreter used by QA and notify QA to re-run (recommended).
   - Commands to run on the workspace host (run as the same user/environment that will run tests):
     - /opt/miniconda3/envs/testbed/bin/python -m pip install pytest
     - /opt/miniconda3/envs/testbed/bin/python -c "import pytest; print(pytest.__version__)"
     - /opt/miniconda3/envs/testbed/bin/python -m pytest --version
   - Then ask QA to run:
     - /opt/miniconda3/envs/testbed/bin/python -m pytest --collect-only tests/forms_tests/tests/test_media.py -q
     - /opt/miniconda3/envs/testbed/bin/python -m pytest tests/forms_tests/tests/test_media.py::FormsMediaTestCase::test_media_deduplication -q
     - (and the other failing tests listed by QA)
B) Engineer: Run DISCOVERY and targeted tests locally in a matching environment and paste raw pytest outputs (collect-only and test run stdout/stderr) on the project board for QA to inspect.

Notes:
- Do not declare PROJECT COMPLETE until QA returns QA_VERDICT: verified: true and PM confirms a non-empty patch exists (read_patch_diff already shows a non-empty patch).
- If helpful, Engineer may optionally apply the small heapq/deque optimization to the merge selection to improve performance before QA re-runs (non-blocking).

Contact: Project Manager (Alice) for coordination once the environment is fixed or test outputs are posted.
