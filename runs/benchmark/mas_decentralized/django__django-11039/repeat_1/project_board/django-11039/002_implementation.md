Engineer: Charlie

Status: Fix implemented and committed locally.

Implementation details:
- File changed: django/core/management/commands/sqlmigrate.py
- Change: Previously, sqlmigrate always wrapped its output in BEGIN/COMMIT when migration.atomic was True. This caused BEGIN/COMMIT to be emitted even for backends that do not support transactional DDL.
- Fix: Set self.output_transaction = migration.atomic and connection.features.can_rollback_ddl so that the outer BEGIN/COMMIT is only added when the migration is atomic and the database backend supports rolling back DDL.

Commit:
- Commit message: "Fix sqlmigrate: only wrap output in transaction if migration is atomic and DB can rollback DDL"
- Local commit recorded in repository (see git log in workspace).

Notes:
- I made a minimal one-line change to the command implementation and committed it.
- I could not run pytest inside this container because pytest is not installed; please run the targeted tests in CI or locally.
