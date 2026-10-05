Engineer implemented changes in src/_pytest/python.py to include fixture scope in `--fixtures` output. Details:

- Show scope for fixtures only when scope != 'function'.
- Append " [<scope> scope]" after the fixture name in both normal and verbose modes.
- Ran the two failing tests locally; one passed and another passed in verbose mode according to engineer's report.

Next: Send patch to CodeReviewer for review.