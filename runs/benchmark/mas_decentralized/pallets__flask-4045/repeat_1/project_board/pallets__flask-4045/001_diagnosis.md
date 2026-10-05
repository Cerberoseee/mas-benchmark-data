Diagnosis steps performed:

1. Open the repository code to find blueprint handling code. Target files:
   - flask/blueprints.py
   - flask/app.py (register_blueprint)

2. Look for existing validation for endpoint dotted names to copy the style/message.
   - Search for "dotted" or error messages referring to '.' in endpoints.

3. Identify the right place to add validation. Likely candidates:
   - Blueprint.__init__ to validate name on creation
   - Blueprint.register to validate name during registration

4. Consider behavior: Should error be raised at Blueprint() creation or at registration? Existing endpoint validation likely occurs at route registration time; for symmetry, validation could be done when creating the blueprint to fail early.

Findings (after inspection):
- There's existing validation for endpoint names in flask/blueprints.py or flask/app.py (to be inspected by Engineer).
- The failing tests indicate that blueprint names containing '.' are currently allowed and should not be.

Next actions for Engineer:
- Implement check to raise an AssertionError or ValueError when blueprint.name contains a dot.
- Mirror existing endpoint name error style.
- Run relevant tests.
