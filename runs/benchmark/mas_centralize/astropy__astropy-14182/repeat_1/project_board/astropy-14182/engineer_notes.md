Engineer implemented a change in astropy/io/ascii/rst.py

Summary of changes:
- RST.__init__ now accepts header_rows kwarg and passes it to FixedWidth.
- Sets self.header.header_rows and self.data.header_rows when provided.
- Adjusts self.data.start_line when header_rows present.
- RST.write updated to recompose lines with top/bottom borders and header_rows.

Patch file present: yes (read via read_patch_diff)

Next: Send to CodeReviewer for quick review per workflow.