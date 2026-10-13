# Security and Reliability

## 1. Authentication

- Use a maintained Google OAuth/OIDC integration compatible with the existing project.
- Validate OAuth state and use PKCE where supported and appropriate.
- Validate identity token issuer, audience, expiry, and required claims.
- Keep client secrets on the server.
- Restrict redirect URIs to approved values.
- Define session expiry and logout behavior.
- Do not request Google Drive API scopes unless Drive access is an explicit requirement.

## 2. Authorization

- The server derives identity from a trusted session/token.
- Every file/folder read, update, delete, and download must enforce authorization.
- Do not trust `ownerId`, user IDs, or permission flags supplied by the client.
- Test attempts to access another user's resources by changing IDs.
- Apply authorization in a consistent backend boundary, not only in UI components.

## 3. Upload safety

- Enforce maximum upload size at both applicable infrastructure and application layers.
- Allow only product-approved file types.
- Do not rely exclusively on client-supplied filename or MIME type.
- Generate internal storage keys instead of using user filenames as paths.
- Prevent path traversal and unsafe path construction.
- Consider malware scanning or content inspection if the deployment risk and product requirements warrant it.
- Stream or bound memory use for large files.
- Avoid serving potentially dangerous content inline unless explicitly safe and required.
- Rate-limit expensive or abuse-prone operations according to existing conventions.

## 4. Secrets and privacy

- Use environment variables or the project's secret-management system.
- Commit only placeholder examples.
- Never log OAuth secrets, tokens, session cookies, or document contents.
- Avoid leaking internal storage paths and stack traces.
- Apply least privilege to database and storage credentials.

## 5. Reliability and consistency

- Define behavior for database outages, storage outages, timeouts, and interrupted uploads.
- Avoid false success responses.
- Plan cleanup/reconciliation for orphaned files or metadata.
- Make retry behavior deliberate; avoid accidental duplicate operations.
- Ensure deletion rules are explicit and testable.
- Use graceful shutdown and existing logging conventions.

## 6. Operations

Document:
- Required environment variables.
- Storage persistence and backup expectations.
- Recovery and cleanup procedures.
- Log fields and sensitive fields that must be excluded.
- Health checks if the existing application supports them.
- Deployment-specific upload limits and timeout requirements.

## 7. Security acceptance checklist

- [ ] Unauthenticated users cannot access private endpoints.
- [ ] Cross-user reads and mutations are rejected.
- [ ] Upload size/type rules are enforced server-side.
- [ ] User filenames cannot escape the storage boundary.
- [ ] OAuth secrets are not shipped to the frontend.
- [ ] Errors do not expose secrets or stack traces.
- [ ] Logs exclude tokens and file contents.
- [ ] Storage/database partial failures have defined handling.
- [ ] Security-relevant cases have automated tests.
