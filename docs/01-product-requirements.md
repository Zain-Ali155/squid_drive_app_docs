# Product Requirements

## 1. Product vision

Build a lightweight, secure, maintainable document-management mini app inside the existing Squid project. It should offer core file-and-folder workflows without trying to reproduce all Google Drive features.

## 2. Goals

- Let users authenticate using Google SSO.
- Let each user manage their own files and folders.
- Make upload, browse, search, download, rename, and delete workflows clear.
- Keep frontend, backend, business rules, persistence, and storage responsibilities separate.
- Reuse suitable packages and conventions already present in the repository.
- Provide tests, documentation, predictable errors, and secure defaults.

## 3. MVP scope

### Authentication and access
- Google sign-in and sign-out.
- Protected application and API access.
- Server-side authorization for each file/folder operation.
- Clear handling of failed or expired authentication.

### Files
- Upload a file.
- List files and view metadata.
- Download an authorized file.
- Rename and delete files.
- Enforce file-size and file-type policies.
- Show upload progress/status where the selected implementation supports it.

### Folders
- Create folders and nested folders.
- Browse folder contents.
- Rename and delete folders according to documented deletion rules.
- Show breadcrumbs and return to parent folders.

### Search and user experience
- Search file and folder names within the authenticated user's permitted scope.
- Handle loading, empty, no-results, success, and error states.
- Responsive, keyboard-accessible interface.

## 4. Out of scope for the MVP

Unless approved as a separate follow-up:
- Real-time collaboration and simultaneous editing.
- Google Drive synchronization.
- Public links and external sharing.
- File version history.
- OCR, document previews for every file type, and content indexing.
- Billing, paid plans, and complex quotas.
- Microservices, queues, and distributed caching.

## 5. Users and permissions

- **Authenticated user:** manages only resources they own or have explicitly been granted access to.
- **Unauthenticated visitor:** cannot access private files or protected APIs.
- **Administrator:** do not introduce special admin privileges unless the existing product requires and defines them.

## 6. Functional requirements

- FR-01: User can sign in with Google.
- FR-02: User can securely sign out.
- FR-03: User can upload an allowed file within configured limits.
- FR-04: User can list and inspect their files.
- FR-05: User can download an authorized file.
- FR-06: User can rename and delete their files.
- FR-07: User can create, list, open, rename, and delete folders.
- FR-08: User can navigate nested folders.
- FR-09: User can search within their authorized scope.
- FR-10: System validates requests on the server.
- FR-11: System gives consistent, useful error feedback.
- FR-12: System does not disclose another user's private resource metadata.

## 7. Non-functional requirements

- **Security:** enforce server-side authorization, safe upload handling, secret management, and secure authentication.
- **Maintainability:** clear modules, consistent conventions, meaningful tests, and documented decisions.
- **Reliability:** handle database/storage failures and avoid misleading success responses.
- **Performance:** use indexes, pagination, bounded uploads, and streaming where suitable.
- **Accessibility:** keyboard operation, visible focus, labels, and adequate contrast.
- **Portability:** configuration through environment variables; no secrets committed.
- **Observability:** useful structured logs without secrets or file contents.

## 8. Product decisions to confirm during discovery

- Existing authentication/session approach and whether Google SSO already exists.
- Existing file-storage service, if any.
- Allowed file types and maximum file size.
- Whether folders can be deleted only when empty or recursively.
- Whether deleted resources are permanently deleted or moved to trash.
- Whether the app supports one organization or multiple tenants.
- Deployment platform and storage persistence requirements.

Do not silently invent business rules for unresolved decisions. Record assumptions and ask only when a decision blocks safe implementation.
