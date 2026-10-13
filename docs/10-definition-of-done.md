# Definition of Done

A story is Done only when all applicable checks below are satisfied.

## Functional
- [ ] Acceptance criteria are met.
- [ ] Success and failure behavior are defined.
- [ ] User-visible feedback is truthful and useful.
- [ ] Edge cases and invalid input are handled.

## Architecture
- [ ] Responsibilities remain clearly separated.
- [ ] No unnecessary cross-module coupling was introduced.
- [ ] Existing conventions and packages were reused where suitable.
- [ ] No unrelated feature was changed without justification.
- [ ] No unnecessary dependency or abstraction was added.

## Security
- [ ] Server-side validation is present.
- [ ] Authentication and authorization are enforced where required.
- [ ] Cross-user resource access is tested.
- [ ] Secrets and private data are not exposed in responses or logs.
- [ ] File handling is safe and bounded where applicable.

## Quality
- [ ] Relevant automated tests were added/updated and run.
- [ ] Type checks pass.
- [ ] Lint/format checks pass.
- [ ] Build passes.
- [ ] Existing relevant tests and features remain operational.

## Documentation
- [ ] Setup/configuration docs are updated if needed.
- [ ] Architecture decisions and assumptions are recorded.
- [ ] Limitations are documented.

## Reporting
- [ ] Actual files changed are listed.
- [ ] Test/build commands and results are recorded.
- [ ] Failures and skipped checks are disclosed.
- [ ] Story status reflects verified work, not just file creation.
