Ticket: INFRA - Ensure pytest is available in the test harness

Description:
QA could not run pytest in the harness environment; attempts to run pytest failed with "bash: line 1: pytest: command not found" and "No module named pytest" when invoking python -m pytest. This blocks verification of the engineer's patch for sympy#12171.

Acceptance criteria:
- pytest is installed in the Python environment used by the QA runner (the same interpreter used to execute tests).
- Running the following in the harness succeeds and pytest is runnable:
  - /opt/miniconda3/envs/testbed/bin/python -m pip install pytest
  - /opt/miniconda3/envs/testbed/bin/python -m pytest --collect-only sympy/printing/tests/test_mathematica.py::test_Derivative -q
- Document which interpreter and PATH the QA runner will use so QA can call pytest consistently.

Notes:
- QA attempted a pip install but python -m pytest still reported "No module named pytest"; ensure pip targets the same interpreter and environment activated by the QA job.
- If the harness uses an isolated container image, bake pytest into the image or add a reproducible step that installs pytest before tests run.

Assign to: CI/Infra team
Priority: High (blocks verification)
