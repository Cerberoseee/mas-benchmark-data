Ticket: Implement default logging format change

Goal: Modify the DEFAULT_LOG_FORMAT constant to include the logger name.

Tasks:
- Update DEFAULT_LOG_FORMAT in the logging configuration module (likely _pytest/logging.py or similar) to "%(levelname)-8s %(name)s:%(filename)s:%(lineno)d %(message)s" or similar per consensus.
- Run full test suite subset for logging tests and iterate based on failures.
- Keep change minimal: only edit the constant and any immediate formatting helpers; avoid broader refactors.

Owner: Engineer
Estimate: 1-2h
