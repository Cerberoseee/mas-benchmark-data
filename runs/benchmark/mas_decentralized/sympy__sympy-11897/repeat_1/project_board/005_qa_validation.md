Title: QA validation for LaTeX printer fixes

Description:
Run the test suite (or a focused subset covering printing) to validate the fixes. Pay particular attention to:
- test_latex_Piecewise (previously failing)
- test_latex_Mul and related printing tests

Assignee: QA
Priority: High

Instructions:
- Run pytest and provide QA_VERDICT block with verified: true/false, failing_ids if any, and notes.
- If verified: true, include confirmation that the engineer's patch is non-empty (board read of patch.diff will be used).
