Title: Coordination/Workflow

Flow:
1. Engineer implements change (001-implementation)
2. Engineer updates tests (002-tests)
3. CodeReviewer reviews patch
4. QA runs tests and validates (transfer to QA)
5. ProjectManager confirms QA_VERDICT and marks complete

Roles:
- Engineer: implement and update tests/docs
- CodeReviewer: quick review of scope
- QA: run failing tests and full test suite subset

