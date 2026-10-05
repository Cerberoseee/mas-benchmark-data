Status: actioned by Engineer (Charlie)

Summary:
- Implemented a minimal fix in django/core/management/commands/sqlmigrate.py to only wrap SQL output in BEGIN/COMMIT when the migration is atomic AND the database backend reports it can rollback DDL.
- This avoids showing transaction markers for backends that cannot rollback DDL.
- Change: set self.output_transaction = migration.atomic and connection.features.can_rollback_ddl

Validation performed:
- Installed pytest and pytest-django into the workspace environment so QA can run tests.
- Ran pytest collection and targeted test commands. Collection now proceeds to Django import steps but fails because pytest-django cannot import the test settings module test_sqlite in this environment.
- The original QA blocker (pytest missing) is resolved; the remaining collection error is an environment/test-settings issue, not a code failure.

Commit:
- Committed locally: fix(sqlmigrate): only wrap SQL output for atomic migrations when DB can rollback DDL

Next steps for QA/PM:
- Re-run the requested verification commands with the workspace PYTHONPATH set so pytest-django can find the test settings module test_sqlite, or instruct me to add a minimal test_sqlite settings module into the repo to enable collection.

Notes:
- I kept the change minimal and limited to the single-line logical condition.
- If you want, I can attempt to add a tiny test settings module to allow full collection and a targeted test run; confirm if you want me to proceed.

Engineer: Charlie