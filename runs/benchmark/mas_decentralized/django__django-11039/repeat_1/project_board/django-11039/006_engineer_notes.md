Engineer: Charlie

Actions taken:
- Applied one-line fix to django/core/management/commands/sqlmigrate.py: self.output_transaction = migration.atomic and connection.features.can_rollback_ddl
- Committed change with message: Fix sqlmigrate: only output transaction when backend supports rollback of DDL

Validation attempts:
- Installed pytest and pytest-django; attempted to collect and run the targeted test but collection fails at import because Django settings are not configured in this environment (tests import models at module scope). This is an environment issue for CI, not the code change.

Notes and next steps:
- Change is minimal and low-risk. Recommend running tests in CI or environment with DJANGO_SETTINGS_MODULE configured, or adding a unit test to mock can_rollback_ddl.

Status: implemented and committed; handing off to ProjectManager for QA/CI verification.
