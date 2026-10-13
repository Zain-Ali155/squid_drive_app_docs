# API and Data Design

> Draft contracts only. Match the existing API versioning, response envelope, and naming conventions after discovery.

## 1. API design rules

- Use the existing API prefix and response conventions.
- Authenticate and authorize on the server.
- Validate all parameters and request bodies.
- Use consistent status codes and safe error messages.
- Do not accept owner IDs from clients as proof of ownership.
- Bound list results and upload size.
- Avoid exposing storage keys or internal filesystem paths.

## 2. Potential endpoints

| Method | Example route | Purpose |
|---|---|---|
| GET | `/api/documents` | List current user's documents; support pagination and optional folder filter |
| POST | `/api/documents` | Upload a document using the selected multipart convention |
| GET | `/api/documents/:id` | Get authorized metadata |
| GET | `/api/documents/:id/download` | Download an authorized document |
| PATCH | `/api/documents/:id` | Rename/update permitted metadata |
| DELETE | `/api/documents/:id` | Delete or move to trash according to product policy |
| GET | `/api/folders` | List authorized folders |
| POST | `/api/folders` | Create a folder |
| GET | `/api/folders/:id/contents` | List a folder's contents |
| PATCH | `/api/folders/:id` | Rename a folder |
| DELETE | `/api/folders/:id` | Delete according to documented folder policy |
| GET | `/api/search` | Search authorized files and folders |

These routes are proposals, not instructions to duplicate routes already present. Inspect the existing application first.

## 3. Document metadata

Potential fields:
- `_id`
- `ownerId` or the existing equivalent identity reference
- `name` (display name; validate length and characters)
- `sizeBytes`
- `mediaType` (server-detected or safely validated)
- `storageKey` (internal; never return unnecessarily)
- `folderId` (optional root/parent relationship)
- `createdAt`
- `updatedAt`
- optional deletion marker/timestamp if trash is approved

Do not store arbitrary file content in the metadata record. Choose the storage mechanism after inspecting existing integrations.

## 4. Folder metadata

Potential fields:
- `_id`
- `ownerId`
- `name`
- `parentFolderId` (nullable for root)
- `createdAt`
- `updatedAt`
- optional deletion marker/timestamp if trash is approved

Validate parent ownership and reject cycles or invalid relationships.

## 5. Indexing

Consider indexes based on actual query patterns, such as:
- owner + folder + updated/created timestamp
- owner + normalized name for search
- parent folder + owner for folder browsing

Do not add indexes speculatively. Inspect queries, test expected workloads, and confirm indexes do not create unintended uniqueness constraints.

## 6. Upload and storage consistency

MongoDB metadata and file storage may not share a transaction. Define a failure strategy, for example:
1. Validate user, file policy, and target folder.
2. Write the file using a safe generated storage key.
3. Persist metadata.
4. If metadata persistence fails, attempt storage cleanup.
5. Log and provide a reconciliation path if cleanup fails.

Choose the exact sequence based on the storage provider. Never report success until the operation reaches its defined successful state.

## 7. Pagination and search

- Set a maximum page size.
- Validate page/cursor input.
- Avoid unbounded full-collection queries.
- Scope queries to the authenticated user's permitted resources.
- Define matching and case-sensitivity rules.
- Add indexes only after confirming the query patterns.
