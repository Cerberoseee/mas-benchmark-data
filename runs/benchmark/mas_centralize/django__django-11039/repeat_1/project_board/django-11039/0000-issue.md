Title: sqlmigrate wraps output in BEGIN/COMMIT on non-transactional DBs

Repository: django/django
Issue: sqlmigrate wraps it's outpout in BEGIN/COMMIT even if the database doesn't support transactional DDL

Summary

The sqlmigrate command currently decides to wrap generated SQL with an outer BEGIN/COMMIT block when the migration is atomic (Migration.atomic). However, for databases that do not support transactional DDL, wrapping in BEGIN/COMMIT is incorrect. The fix is to also check connection.features.can_rollback_ddl when choosing to wrap SQL in transactions.

Steps

1. Update code in the sqlmigrate command to set self.output_transaction = migration.atomic and connection.features.can_rollback_ddl (i.e. both must be true).
2. Add a test in tests/migrations/test_commands.py to mock connection.features.can_rollback_ddl=False and assert sqlmigrate output does not include BEGIN/COMMIT even if migration.atomic is True.

Constraints

- Minimal surface change.
- Tests must not modify actual database capabilities – use mocking.

Assignees

- Engineer: implement the fix and tests
- QA: run test suite and validate

Notes

Original report suggests basing new test on existing non-atomic migration test by mocking can_rollback_ddl.
