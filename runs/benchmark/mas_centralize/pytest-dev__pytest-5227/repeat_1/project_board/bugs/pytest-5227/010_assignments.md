Assigned roles:
- Engineer: @alice-engineer
- CodeReviewer: @alice-codereviewer
- QA: @alice-qa

Workflow:
1) Engineer implements minimal change and commits patch.
2) CodeReviewer inspects diff.
3) QA runs failing tests & returns QA_VERDICT.
4) ProjectManager verifies patch exists and QA verified true, then closes ticket.

Notes: Ensure test harness-applied patches are not overwritten and do not modify tests.