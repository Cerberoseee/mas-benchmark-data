Issue: sqlmigrate wraps it's outpout in BEGIN/COMMIT even if the database doesn't support transactional DDL

Repository: django/django
Base commit: d5276398046ce4a102776a1e67dcac2884d80dfe

Goal: Fix sqlmigrate so it only outputs BEGIN/COMMIT when both migration.atomic is True and connection.features.can_rollback_ddl is True. Add a test to cover non-transactional DBs.

Plan:
- Investigate failing test: migrations.test_commands.MigrateTests.test_sqlmigrate_for_non_transactional_databases
- Make minimal code change in management command sqlmigrate to set output_transaction considering connection.features.can_rollback_ddl
- Add test mocking connection.features.can_rollback_ddl = False
- Run tests for migrations.test_commands

Tickets:
- 001_diagnose: Reproduce failing test and locate code
- 002_implementation: Change sqlmigrate to consider can_rollback_ddl
- 003_tests: Add test to cover behavior
- 004_reviewer: Code review
- 005_qa: QA validation

Routing:
- Engineer: implement 002 and 003
- CodeReviewer: review
- QA: run targeted tests and report QA_VERDICT

Notes:
- Keep changes minimal and confined to management command and tests.
- Ensure non-empty patch before declaring completion.