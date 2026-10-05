Title: 0005-engineer - Engineer implementation notes and patch

Summary:
I implemented host and subdomain columns in the `flask routes` CLI command. Changes made in src/flask/cli.py.

Key points:
- Detect presence of Rule.host and Rule.subdomain across rules.
- Add Host and Subdomain columns conditionally (only when any rule has them) to keep output concise.
- Compute column widths and build a dynamic row format string.
- For each rule, populate host/subdomain values using getattr(rule, "host") and getattr(rule, "subdomain").

Why minimal change:
- No tests modified; behavior limited to CLI output generation.

Next:
- Handoff to CodeReviewer for review.
