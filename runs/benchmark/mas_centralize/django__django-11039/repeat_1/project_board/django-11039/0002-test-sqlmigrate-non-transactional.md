Title: Add test for sqlmigrate with non-transactional DDL

Task

Add a test in tests/migrations/test_commands.py named test_sqlmigrate_for_non_transactional_databases. The test should mock connection.features.can_rollback_ddl to False and call the sqlmigrate command for an atomic migration, asserting that the output does not contain BEGIN/COMMIT but still contains the migration SQL.

Notes

- Base on existing test_sqlmigrate_for_non_atomic_migration in the same file.
- Use unittest.mock.patch to override connection.features.can_rollback_ddl.
