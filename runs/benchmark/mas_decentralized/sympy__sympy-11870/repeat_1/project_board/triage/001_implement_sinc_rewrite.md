Implementation ticket: add rewrite path so expressions equivalent to sin(x)/x become sinc(x) when rewrite(sinc) is requested.

Tasks:
- Modify the rewrite machinery for Sin or Sinc so that rewrite('sinc') handles sin(x)/x -> sinc(x).
- Prefer to add this in the existing rewrite mapping in sympy/functions/elementary/trigonometric.py or where Sinc is defined.
- Add minimal unit tests if necessary (but harness already contains failing test).
- Ensure no changes to tests in the repo.

Deliverable:
- A patch implementing the rewrite.
- Short explanation of why the change is minimal and safe.
