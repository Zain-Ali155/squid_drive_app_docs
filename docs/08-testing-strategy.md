# Testing Strategy

## 1. Framework policy

Inspect existing test configuration first. Reuse the configured framework. Use Jest only if it is already installed or is selected after checking compatibility and project conventions. Avoid duplicate testing frameworks.

## 2. Test layers

### Unit tests
Test pure validation, business rules, and services independently. Mock repositories and storage when that makes tests focused and reliable.

### Integration tests
Test API routes, middleware, persistence, and service/repository interactions using isolated test configuration and data.

### UI tests
Reuse existing frontend testing tools. Focus on key interactions, loading/error states, and accessible controls. Do not add a large UI test stack without justification.

### End-to-end tests
Add only if the repository already supports them or the project risk justifies the extra setup. Cover essential user journeys.

## 3. Minimum coverage scenarios

### Authentication
- Successful Google callback.
- User cancels consent.
- Invalid or expired authentication state.
- Protected route without authentication.
- Logout invalidates the chosen session/token state.

### Authorization
- User accesses their own resource.
- User attempts to read another user's resource.
- User attempts to rename/delete/download another user's resource.
- Forged owner ID in request payload is ignored/rejected.

### Files
- Valid upload.
- Unsupported type.
- Oversized upload.
- Storage failure.
- Metadata persistence failure.
- Authorized download.
- Missing file.
- Rename success and invalid name.
- Delete success and cleanup failure.

### Folders
- Create root folder.
- Create nested folder.
- Parent belongs to another user.
- Invalid parent reference.
- Rename folder.
- Delete empty and non-empty folder according to selected policy.
- Attempted cycle or invalid hierarchy.

### Search and UI
- Empty search and no results.
- Search results are user-scoped.
- Loading, error, and retry states.
- Responsive and keyboard-critical interactions.

## 4. Test quality

- Tests should be deterministic and isolated.
- Do not use production credentials or production data.
- Clean up test records and temporary files.
- Avoid tests that pass by swallowing exceptions.
- Keep assertions tied to requirements.
- Report skipped, failed, and passed tests accurately.

## 5. Release checks

Run the repository's actual scripts for:
- Unit/integration tests.
- Type checking.
- Linting/format checks.
- Production build.

Do not invent command names; inspect `package.json` first. Record any pre-existing failures separately from new failures.
