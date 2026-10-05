Engineer: Charlie
Status: Fixed (pending review)

Summary:
- Adjusted sqlmigrate to only wrap output with BEGIN/COMMIT when migration.atomic is True and connection.features.can_rollback_ddl is True.

Details:
- Modified: django/core/management/commands/sqlmigrate.py
- Commit: Fix sqlmigrate: only wrap SQL in BEGIN/COMMIT when backend can rollback DDL (django-11039)

Testing:
- The targeted failing test is tests/migrations/test_commands.py::MigrateTests::test_sqlmigrate_for_non_transactional_databases.
- Note: pytest is not available in this execution environment, so I could not run the test here. The change is minimal and intended to be exercised by mocking connection.features.can_rollback_ddl in the test.

Next steps:
- Please run the targeted tests in CI or a dev environment with pytest available.
- Code reviewer: please review the one-line behavioral change.
- QA: run the listed Fail-to-pass and Pass-to-pass tests.
