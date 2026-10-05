Handoff to Engineer

Please implement the fix described in 002_implement_fix.md. Key points:
- Preserve leading '*' characters in parameter names when merging typehints into parameter descriptions.
- Do not create duplicate param nodes; update existing ones.
- Ensure no inline markup warnings are produced for '*args' and '**kwargs'.

Start by running the two failing tests and a collection of related napoleon/autodoc tests. Commit patch.diff with minimal changes.

Coordination:
- After implementation, push patch and mark ready for code review.
