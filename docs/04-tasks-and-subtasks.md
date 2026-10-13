# Tasks and Subtasks

This is an implementation-oriented task breakdown. The agent must verify real file paths and repository conventions during discovery before using or creating any path.

## E01 — Foundation and Architecture

### E01-S01 — Review existing architecture
- **T01:** Inspect repository structure.
  - ST01: Inspect root and app-level package manifests and lockfiles.
  - ST02: Map frontend routes and shared components.
  - ST03: Map Express routes, middleware, controllers, services, and repositories.
- **T02:** Inventory reusable infrastructure.
  - ST01: Identify authentication and session packages.
  - ST02: Identify validation and test frameworks.
  - ST03: Identify MongoDB models, logging, error handling, and storage integrations.
- **T03:** Write discovery report.
  - ST01: Record conventions and integration points.
  - ST02: Record gaps, risks, and questions.
  - ST03: Propose repository-specific module boundaries.

### E01-S02 — Establish module boundaries
- **T01:** Define file/document and folder responsibilities.
  - ST01: Define service responsibilities.
  - ST02: Define repository contracts.
  - ST03: Define storage adapter contract if needed.
- **T02:** Define dependency direction.
  - ST01: Document allowed imports.
  - ST02: Identify forbidden cross-module internal access.
  - ST03: Add lightweight boundary checks only if project conventions support them.

### E01-S03 — Configuration
- **T01:** Define required environment configuration.
  - ST01: Document each variable and purpose.
  - ST02: Validate required settings at startup.
  - ST03: Ensure example files contain placeholders only.

## E02 — Google SSO and Authorization

### E02-S01 — Google sign-in
- **T01:** Select the integration.
  - ST01: Inspect existing auth packages.
  - ST02: Compare compatible maintained options if needed.
  - ST03: Record the selected flow and rationale.
- **T02:** Configure OAuth/OIDC.
  - ST01: Configure approved client ID, secret, and redirect URI.
  - ST02: Validate state and applicable PKCE protections.
  - ST03: Validate issuer, audience, expiry, and identity claims through the trusted flow.
- **T03:** Implement sign-in and failure handling.
  - ST01: Implement callback behavior.
  - ST02: Handle denied consent and invalid callback.
  - ST03: Add tests for success and failure.

### E02-S02 — Sign-out
- **T01:** Implement the chosen session/token invalidation behavior.
  - ST01: Clear/invalidate session state as appropriate.
  - ST02: Verify protected endpoints reject the old session.
  - ST03: Add logout tests.

### E02-S03 — Authorization
- **T01:** Define resource ownership rules.
  - ST01: Derive user identity from trusted auth context.
  - ST02: Define ownership filters for each repository operation.
  - ST03: Define consistent not-found/forbidden behavior.
- **T02:** Add access-control tests.
  - ST01: Test unauthenticated access.
  - ST02: Test cross-user read.
  - ST03: Test cross-user update/delete/download.

## E03 — File Management

### E03-S01 — Upload
- **T01:** Define file metadata.
  - ST01: Define owner, name, size, media type, storage key, timestamps, and optional folder reference.
  - ST02: Define indexes and validation rules.
- **T02:** Implement storage integration.
  - ST01: Inspect existing provider.
  - ST02: Select and document provider if missing.
  - ST03: Implement bounded/streaming upload as appropriate.
- **T03:** Implement upload service and endpoint.
  - ST01: Validate authentication and authorization.
  - ST02: Validate size and permitted types.
  - ST03: Coordinate storage and metadata persistence.
  - ST04: Handle cleanup/reconciliation after partial failure.
- **T04:** Test upload.
  - ST01: Test valid upload.
  - ST02: Test invalid type and oversize file.
  - ST03: Test database/storage failure.

### E03-S02 — List and metadata
- **T01:** Implement ownership-scoped listing.
  - ST01: Add pagination or a bounded result limit.
  - ST02: Return only required metadata.
  - ST03: Add repository tests.
- **T02:** Implement details UI.
  - ST01: Display supported metadata.
  - ST02: Add loading, empty, and error states.

### E03-S03 — Download
- **T01:** Implement authorized download.
  - ST01: Verify ownership before reading storage.
  - ST02: Set safe response headers and filename.
  - ST03: Handle missing storage objects.
- **T02:** Test download.
  - ST01: Test valid download.
  - ST02: Test missing resource.
  - ST03: Test cross-user access.

### E03-S04 — Rename
- **T01:** Implement validated rename service and API.
  - ST01: Validate name and resource ownership.
  - ST02: Keep metadata consistent.
  - ST03: Test success and invalid requests.

### E03-S05 — Delete
- **T01:** Implement deletion policy.
  - ST01: Decide hard delete or trash.
  - ST02: Define metadata/storage cleanup order.
  - ST03: Define retry/reconciliation for partial failure.
- **T02:** Test deletion.
  - ST01: Test authorized deletion.
  - ST02: Test cross-user deletion.
  - ST03: Test storage cleanup failure.

## E04 — Folder Management

### E04-S01 — Create folder
- **T01:** Define folder schema and indexes.
  - ST01: Define owner, name, parent, timestamps.
  - ST02: Define root-folder representation.
- **T02:** Implement create operation.
  - ST01: Validate name and parent ownership.
  - ST02: Reject invalid parent relationships.
  - ST03: Add tests.

### E04-S02 — Browse folders
- **T01:** Implement folder contents query.
  - ST01: Scope query to authenticated owner.
  - ST02: Return bounded file/folder lists.
  - ST03: Test nested folders and isolation.
- **T02:** Implement breadcrumbs.
  - ST01: Derive hierarchy from trusted backend data.
  - ST02: Add parent navigation and empty states.

### E04-S03 — Rename folder
- **T01:** Implement ownership-checked rename.
  - ST01: Validate input.
  - ST02: Preserve child relationships.
  - ST03: Test success and failure.

### E04-S04 — Delete folder
- **T01:** Implement documented deletion policy.
  - ST01: Enforce empty-only or recursive behavior.
  - ST02: Check ownership for all affected resources.
  - ST03: Handle partial failures safely.
- **T02:** Test folder deletion edge cases.
  - ST01: Empty folder.
  - ST02: Non-empty folder.
  - ST03: Cross-user child/reference cases.

## E05 — Search and Navigation

### E05-S01 — Search
- **T01:** Implement validated search query.
  - ST01: Define case-sensitivity and matching behavior.
  - ST02: Scope search to authorized resources.
  - ST03: Limit results and protect against expensive queries.
- **T02:** Optimize search.
  - ST01: Inspect query patterns.
  - ST02: Add and verify suitable indexes.
  - ST03: Record explain-plan findings where useful.
- **T03:** Add search UI and tests.
  - ST01: Add input and loading feedback.
  - ST02: Add empty/no-results/error states.
  - ST03: Test special characters and access isolation.

### E05-S02 — Breadcrumbs
- **T01:** Implement current-path display.
  - ST01: Handle root and nested folders.
  - ST02: Handle missing/deleted parent.
  - ST03: Test responsive behavior.

## E06 — UI/UX

### E06-S01 — Dashboard
- **T01:** Inspect existing theme and components.
  - ST01: Identify styling framework and fonts.
  - ST02: Identify existing icon, dialog, and toast components.
- **T02:** Build workspace layout.
  - ST01: Build navigation.
  - ST02: Build file/folder listing.
  - ST03: Build responsive states.
- **T03:** Add UI states.
  - ST01: Add loading and empty states.
  - ST02: Add error and retry behavior.
  - ST03: Add success feedback.

### E06-S02 — Resource actions
- **T01:** Build action menus and dialogs.
  - ST01: Add rename dialog.
  - ST02: Add delete confirmation.
  - ST03: Prevent duplicate submissions.
  - ST04: Show truthful success/failure feedback.

### E06-S03 — Accessibility
- **T01:** Review keyboard behavior.
  - ST01: Check focus visibility and order.
  - ST02: Check dialogs and menus.
  - ST03: Check labels, contrast, and reduced motion.

## E07 — Security and Reliability

### E07-S01 — Safe uploads
- **T01:** Enforce upload limits and file policies.
  - ST01: Configure maximum size and permitted types.
  - ST02: Do not trust client MIME type or filename.
  - ST03: Prevent path traversal and unsafe path construction.
- **T02:** Review resource use.
  - ST01: Use streaming/bounded buffering where appropriate.
  - ST02: Ensure failed uploads are cleaned up or reconciled.

### E07-S02 — Failure handling
- **T01:** Standardize errors.
  - ST01: Reuse existing error conventions.
  - ST02: Map expected failures to safe responses.
  - ST03: Keep stack traces and secrets out of client responses.
- **T02:** Add safe diagnostics.
  - ST01: Log operation identifiers and useful context.
  - ST02: Exclude tokens, credentials, and file contents.

### E07-S03 — Data integrity
- **T01:** Review relationships and queries.
  - ST01: Enforce owner filters.
  - ST02: Validate parent folder relationships.
  - ST03: Prevent cycles and invalid references.
- **T02:** Review failure recovery.
  - ST01: Document metadata/storage consistency strategy.
  - ST02: Add tests for partial failure and retries where applicable.

## E08 — Testing and Quality

### E08-S01 — Unit tests
- **T01:** Test validation and business services.
  - ST01: Cover success paths.
  - ST02: Cover invalid input.
  - ST03: Cover missing resources and dependency failures.

### E08-S02 — Integration and authorization tests
- **T01:** Test API and persistence workflows.
  - ST01: Test authentication.
  - ST02: Test CRUD and search.
  - ST03: Test cross-user isolation.
- **T02:** Keep tests isolated.
  - ST01: Use test configuration and data cleanup.
  - ST02: Mock external storage/auth where appropriate.

### E08-S03 — Regression and quality checks
- **T01:** Run repository quality commands.
  - ST01: Run tests.
  - ST02: Run type checks and lint.
  - ST03: Run production build.
  - ST04: Report failures and existing baseline issues honestly.

## E09 — Documentation and Delivery

### E09-S01 — Setup guide
- **T01:** Document local setup.
  - ST01: List prerequisites and commands.
  - ST02: Document environment variables with placeholders.
  - ST03: Document Google OAuth setup.

### E09-S02 — Operations and architecture
- **T01:** Document design.
  - ST01: Record module boundaries and decisions.
  - ST02: Document storage/deletion/backup behavior.
  - ST03: List limitations and future work.

### E09-S03 — Delivery report
- **T01:** Summarize implementation.
  - ST01: List completed and incomplete backlog items.
  - ST02: List added dependencies and rationale.
  - ST03: Record actual test/build results.
  - ST04: Record known risks.
