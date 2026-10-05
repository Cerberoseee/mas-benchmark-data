Engineer: Charlie

Status: Implemented fix in django/core/management/commands/sqlmigrate.py

Summary:
- Problem: sqlmigrate wrapped its output in BEGIN/COMMIT even when the database backend could not rollback DDL.
- Fix: set self.output_transaction = migration.atomic and connection.features.can_rollback_ddl so the outer transaction is only added when the migration is atomic and the backend supports DDL rollback.

Commit: local commit recorded in the workspace repository.

Tests: pytest is not available in this container, so I could not execute the targeted tests here. Please run the following tests in CI or a local environment with pytest available:
- tests/migrations/test_commands.py::MigrateTests::test_sqlmigrate_for_non_transactional_databases

Notes: Minimal change to sqlmigrate command (single-line logic update).

Next steps: Code review and QA to run the full migration test set and verify behavior on backends that do not support transactional DDL.
