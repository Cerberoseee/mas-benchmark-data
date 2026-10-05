Task: Implement unit test for non-transactional DB behavior of sqlmigrate

Goal:
- Add a unit test to tests/migrations/test_commands.py that asserts sqlmigrate does NOT wrap SQL output in BEGIN/COMMIT when the migration is atomic but the backend cannot rollback DDL (connection.features.can_rollback_ddl == False).

Test implementation guidance (copy into the existing MigrateTests test case in tests/migrations/test_commands.py):

    def test_sqlmigrate_for_non_transactional_databases(self):
        """sqlmigrate should not wrap output in BEGIN/COMMIT if the DB can't rollback DDL."""
        out = StringIO()
        # Patch the backend feature to indicate it cannot rollback DDL
        with mock.patch.object(connection.features, 'can_rollback_ddl', False):
            call_command('sqlmigrate', 'migrations', '0001_initial', stdout=out)
        sql = out.getvalue()
        # Ensure we do not wrap the output in transaction markers
        self.assertFalse(sql.strip().startswith('BEGIN'))
        self.assertNotIn('COMMIT;', sql)

Notes:
- Use the same test class and style as other tests in the file (unittest.TestCase methods and self.assert* helpers).
- Ensure imports at top of the file include:
    from io import StringIO
    from unittest import mock
    from django.core.management import call_command
    from django.db import connection
  (If these are already present near other sqlmigrate tests, reuse them.)
- Do not modify existing tests besides adding this new test method.

After implementing:
- Commit the change (ensure patch.diff is non-empty).
- Transfer to CodeReviewer for quick review.
- After review approval, request QA to run the targeted test(s) and report QA_VERDICT.

Assign to: Engineer
Estimated effort: small (~15-30 minutes).