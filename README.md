# Squid Document Management Mini App

Planning and architecture documentation for a lightweight, independent document-management application inspired by Google Drive.

## Purpose

Provide a secure place for authenticated users to upload, organize, search, download, rename, and delete their files and folders.

## Technology

- Frontend: Next.js + TypeScript
- Backend: Node.js + Express + TypeScript
- Database: MongoDB
- Authentication: Google SSO
- Testing: reuse the existing framework; Jest only if suitable and not already configured
- Validation: reuse the existing validation library; evaluate Joi only if needed

## Documentation

1. [Product Requirements](docs/01-product-requirements.md)
2. [Architecture](docs/02-architecture.md)
3. [Epics and Stories](docs/03-epics-and-stories.md)
4. [Tasks and Subtasks](docs/04-tasks-and-subtasks.md)
5. [API and Data Design](docs/05-api-and-data-design.md)
6. [Security and Reliability](docs/06-security-and-reliability.md)
7. [UI and Design System](docs/07-ui-design-system.md)
8. [Testing Strategy](docs/08-testing-strategy.md)
9. [Implementation Roadmap](docs/09-implementation-roadmap.md)
10. [Definition of Done](docs/10-definition-of-done.md)
11. [Architecture Decision Records](docs/adr/README.md)

## Agent workflow

1. Inspect the existing repository and report its actual structure and dependencies.
2. Compare the current codebase with these documents and identify gaps.
3. Present a repository-specific plan and backlog for review.
4. Implement one approved story at a time.
5. Run tests and quality checks and report actual results.

**Important:** These files are a starting plan, not proof that any feature has been implemented. Do not assume example paths or package choices match the repository until inspected.
