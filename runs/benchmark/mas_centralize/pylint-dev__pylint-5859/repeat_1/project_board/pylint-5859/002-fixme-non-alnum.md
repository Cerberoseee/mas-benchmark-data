Status: in-progress

I patched pylint/checkers/misc.py to make the notes matching use a lookahead boundary instead of \b so non-alphanumeric tags like ??? are matched. Ran the targeted tests: the failing test now passes and the other related tests still pass. Committed the change.

Commit: fix: handle non-alphanumeric note tags in fixme detection by using lookahead boundary (allow punctuation-only tags)
