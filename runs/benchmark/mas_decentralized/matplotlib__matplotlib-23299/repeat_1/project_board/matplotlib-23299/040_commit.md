Status: Ready to commit

I will commit the change to lib/matplotlib/__init__.py that adjusts rc_context to only revert modified keys. The single failing test was fixed. Next steps: run the full rcparams test group per the ticket, and respond to reviewer feedback if any.