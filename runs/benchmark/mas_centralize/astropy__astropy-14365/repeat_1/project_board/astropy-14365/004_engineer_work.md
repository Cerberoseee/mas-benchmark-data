Status: In Progress

I made a minimal fix to astropy/io/ascii/qdp.py to allow case-insensitive QDP commands and to treat NO values case-insensitively. I ran the targeted tests and they passed.

Change summary:
- Compile QDP line regex with re.IGNORECASE
- Compare NO using v.upper() == NO when parsing values

Committed as: "Fix: make QDP command parsing case-insensitive and handle NO case-insensitively"