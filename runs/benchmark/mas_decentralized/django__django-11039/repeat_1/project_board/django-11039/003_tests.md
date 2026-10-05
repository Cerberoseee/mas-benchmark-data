Task: Add test for non-transactional DB

Change (detailed):
- Add a test in tests/migrations/test_commands.py that patches connection.features.can_rollback_ddl = False and asserts sqlmigrate doesn't wrap output in BEGIN/COMMIT.

Suggested test snippet (add to tests/migrations/test_commands.py near other sqlmigrate tests):

from io import StringIO
from unittest import mock
from django.core.management import call_command
from django.db import connection

def test_sqlmigrate_for_non_transactional_databases(self):
    out = StringIO()
    # Patch the backend feature to indicate it cannot rollback DDL
    with mock.patch.object(connection.features, 'can_rollback_ddl', False):
        call_command('sqlmigrate', 'migrations', '0001_initial', stdout=out)
    sql = out.getvalue()
    # Ensure we do not wrap the output in a surrounding transaction
    assert not sql.strip().startswith('BEGIN') and 'COMMIT' not in sql

Notes:
- Adapt migration label ('migrations', '0001_initial') to match existing tests in the file; this snippet is illustrative. Reuse patterns from test_sqlmigrate_for_non_atomic_migration.
- Keep the test focused and minimal. Do not modify existing tests unless necessary.

Acceptance:
- New test added and failing before implementation, passing after change.

Assign to: Engineer

QA feedback to include in next run:
QA_VERDICT:
  verified: false
  failing_ids:
    - migrations.test_commands.MigrateTests::test_sqlmigrate_for_non_transactional_databases: test collection failed — pytest not installed in the environment (No module named pytest)
  notes: Test collection failed due to missing pytest; please make pytest available and re-run pytest --collect-only tests/migrations/test_commands.py, then run the targeted test.