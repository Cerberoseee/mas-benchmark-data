Action for Engineer: Add unit test and run QA

Context:
- Implementation change already committed in django/core/management/commands/sqlmigrate.py to only output transaction markers when migration.atomic and connection.features.can_rollback_ddl are both True.
- Code review passed with no blocking findings.
- QA could not run tests due to missing pytest in the environment; see QA_VERDICT below.

QA_VERDICT:
  verified: false
  failing_ids:
    - migrations.test_commands.MigrateTests::test_sqlmigrate_for_non_transactional_databases: test collection failed — pytest not installed in the environment (No module named pytest)
  notes: Test collection failed due to missing pytest; please make pytest available and re-run pytest --collect-only tests/migrations/test_commands.py, then run the targeted test.

Required Engineer tasks (small, focused):
1) Add the new unit test in tests/migrations/test_commands.py. Follow the existing test style (see test_sqlmigrate_for_non_atomic_migration in the same file). Example snippet:

    def test_sqlmigrate_for_non_transactional_databases(self):
        out = StringIO()
        # Patch the backend feature to indicate it cannot rollback DDL
        with mock.patch.object(connection.features, 'can_rollback_ddl', False):
            call_command('sqlmigrate', 'migrations', '0001_initial', stdout=out)
        sql = out.getvalue()
        # Ensure we do not wrap the output in a surrounding transaction
        self.assertFalse(sql.strip().startswith('BEGIN'))
        self.assertNotIn('COMMIT', sql)

Notes:
- Adapt the migration label ('migrations', '0001_initial') to match the existing migration used by other sqlmigrate tests in that file.
- Use unittest-style assertions consistent with the file (self.assertFalse / self.assertNotIn).
- Do not modify existing tests other than adding the new test function.

2) Commit the change and push. Ensure patch.diff is non-empty (it will be).

3) After committing, request CodeReviewer for a quick review. (Given the minimal nature of the change, this should be straightforward.)

4) After review approval, ask QA to re-run:
   - pytest --maxfail=1 --disable-warnings -q --collect-only tests/migrations/test_commands.py
   - pytest -k test_sqlmigrate_for_non_transactional_databases -q

If QA still reports pytest missing, coordinate with infra to make pytest available in the QA environment (python -m pip install pytest) or run tests in a tox/CI environment that has pytest.

Acceptance criteria:
- New test added and passing in QA: QA_VERDICT must report verified: true and no failing_ids.
- CodeReviewer sign-off present.

Assign to: Engineer

Estimated effort: small (adding one test, <30 minutes).