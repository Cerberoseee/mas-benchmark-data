Issue: Merging 3 or more media objects can throw unnecessary MediaOrderConflictWarnings
Repository: django/django
Base commit: 93e892bb645b16ebaf287beb5fe7f3ffe8d10408

Goal: Ensure Media merging preserves intended order without introducing spurious ordering constraints when combining multiple Media objects. Create focused tickets for diagnosis, implement a minimal fix, get code review and QA validation.

Workflow ownership: Alice (Project Manager). Engineer will implement, CodeReviewer will review, QA will validate.
