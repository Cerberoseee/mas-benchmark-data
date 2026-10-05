Status: completed

I (Charlie) updated pylint/checkers/misc.py to handle non-alphanumeric note tags passed via the --notes option. The change uses a lookahead after the tag so punctuation-only tags like ??? are matched.

Committed change: fix: allow non-alphanumeric note tags in --notes option (handle punctuation like ???)
