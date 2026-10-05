Title: Fix sqlmigrate to respect connection.features.can_rollback_ddl

Goal

Change sqlmigrate to only wrap output in BEGIN/COMMIT when both migration.atomic is True and connection.features.can_rollback_ddl is True.

Scope

- Edit management/commands/sqlmigrate.py or appropriate command implementation.
- Add unit test in tests/migrations/test_commands.py.

Acceptance criteria

- New test test_sqlmigrate_for_non_transactional_databases passes.
- No regression in existing migration command tests.

Implementation notes

- Prefer mocking connection.features.can_rollback_ddl in the test.
- Ensure not to alter other behavior (minimal change).
