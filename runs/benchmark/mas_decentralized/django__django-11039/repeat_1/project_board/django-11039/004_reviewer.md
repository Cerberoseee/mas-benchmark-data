Task: Code review for sqlmigrate fix

Checklist:
- Change is minimal and limited to sqlmigrate command and tests.
- Ensure no test files were accidentally modified other than new test.
- Confirm output_transaction is computed using both migration.atomic and connection.features.can_rollback_ddl.
- Confirm tests for migrations pass.

After approval, transfer to QA.