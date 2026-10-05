Escalation: pytest installation required in testbed (urgent)

Summary:
QA cannot verify the engineer's patch because pytest is not importable by the testbed python3 interpreter. Multiple attempts to install pytest via pip from QA failed (python3 still reports "No module named pytest"), indicating pip may be installing into a different Python environment.

Action requested (infra/testbed owner):
1) Install pytest into the exact Python interpreter used by the harness. On the testbed host, run:
   - /opt/miniconda3/envs/testbed/bin/python3 -m pip install --upgrade pip setuptools
   - /opt/miniconda3/envs/testbed/bin/python3 -m pip install pytest
   - Verify installation:
     - /opt/miniconda3/envs/testbed/bin/python3 -c "import pytest; print(pytest.__version__)"

2) If the testbed uses a conda environment differently, activate the correct env and install via conda:
   - conda activate testbed
   - conda install pytest
   - Verify with the correct python binary as above.

3) If network access is restricted, upload a pytest wheel to the workspace and install it using the same python binary:
   - /opt/miniconda3/envs/testbed/bin/python3 -m pip install /path/to/pytest.whl

After pytest is available, QA should re-run the verification steps and report QA_VERDICT:
- pytest --collect-only tests/expressions/tests.py -q
- pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_by_multiline_sql -q
- pytest tests/expressions/tests.py::BasicExpressionsTests::test_order_of_operations -q

Priority: High — blocks merging the fix. Please respond here with confirmation and ETA, and paste the verification command outputs if convenient.
