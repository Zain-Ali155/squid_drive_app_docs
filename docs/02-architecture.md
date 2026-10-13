# Architecture

## 1. Architecture approach

Use a modular monolith unless the existing Squid architecture dictates otherwise. A modular monolith keeps deployment simple while preserving clear module boundaries. Do not introduce microservices for this MVP.

## 2. Technology constraints

- Next.js + TypeScript frontend.
- Node.js + Express + TypeScript backend.
- MongoDB database.
- Google SSO.
- Reuse compatible packages already installed.
- Keep the existing application and unrelated modules working.

## 3. Conceptual request flow

```text
Browser
  |
  v
Next.js UI / Feature Components
  |
  v
API Client
  |
  v
Express Routes
  |
  v
Authentication + Authorization + Validation
  |
  v
Controller
  |
  v
Application Service (business rules)
  |
  +--------------------+
  |                    |
  v                    v
Repository             File Storage Adapter
  |                    |
  v                    v
MongoDB             Configured storage provider
```

The exact implementation must be adapted after repository inspection.

## 4. Responsibilities

### Frontend
- Render screens and reusable UI.
- Handle user interactions and presentation state.
- Call the backend through the existing API client conventions.
- Provide friendly validation and operation feedback.
- Never be the final authority for authorization.

### HTTP/API layer
- Define routes and request/response contracts.
- Authenticate requests.
- Validate input.
- Call application services.
- Map known errors to consistent HTTP responses.

### Application services
- Implement business rules.
- Enforce ownership and folder relationship rules.
- Coordinate metadata and storage operations.
- Avoid framework-specific concerns where practical.

### Repositories
- Encapsulate MongoDB queries and persistence.
- Apply ownership filters to resource queries.
- Use indexes and bounded/paginated queries where appropriate.

### Storage adapter
- Encapsulate file storage operations.
- Provide safe upload, download, and deletion behavior.
- Avoid coupling business logic to a specific provider.
- Do not assume a paid cloud provider without approval.

## 5. Module boundaries

Potential logical modules:
- Authentication
- Documents/files
- Folders
- Storage
- Shared infrastructure (configuration, logging, errors)

These are logical boundaries, not mandatory folder names. Follow existing repository conventions. A module should expose a small public interface; other modules must not reach into its private repositories or internal implementation.

## 6. Design principles

- Separation of Concerns and Single Responsibility.
- Low coupling and high cohesion.
- Dependency inversion where it meaningfully improves testability or provider replacement.
- Open/Closed where future extension is plausible.
- DRY and KISS.
- Encapsulation and explicit module contracts.
- Least privilege and secure defaults.
- Avoid premature abstraction and overengineering.

## 7. File storage decision

Do not store arbitrarily large file contents directly in ordinary MongoDB documents. Inspect existing storage first. If none exists, compare the deployment's persistent disk, MongoDB GridFS, or a compatible object-storage provider. Document cost, persistence, limits, backup, cleanup, and operational implications before selecting. Use streaming or bounded buffering for large files where supported.

## 8. Dependency policy

1. Inspect all relevant `package.json` files and lockfiles.
2. Reuse existing packages when appropriate.
3. Avoid duplicate libraries and unnecessary upgrades.
4. Add a package only when the need is clear, compatibility is checked, and alternatives are documented.
5. Do not add Jest, Joi, Auth.js, Passport, or a UI library blindly; first inspect what is already configured and appropriate.

## 9. Failure consistency

Use the project's established error format if one exists. Distinguish validation, authentication, authorization, not-found, conflict, storage, and unexpected errors. Log diagnostic details safely; return no stack traces or secrets to clients.

## 10. Integration rule

Do not rewrite the existing project. Keep unrelated routes and features unchanged. Identify required integration points and regression tests before implementation.
