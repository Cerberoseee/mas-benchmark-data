Engineer implemented change: updated DEFAULT_LOG_FORMAT in src/_pytest/logging.py to include %(name)s.

Patch summary (from patch.diff):
- Modified DEFAULT_LOG_FORMAT value from "%(filename)-25s %(lineno)4d %(levelname)-8s %(message)s" to "%(levelname)-8s %(name)s:%(filename)s:%(lineno)d %(message)s".

Next steps: Code review, then QA run of affected tests. See tests failing earlier; engineer reports tests now pass locally. Attach patch.diff to board.
