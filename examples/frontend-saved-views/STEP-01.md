# Step 01: SavedView Data Model and REST API

**Project:** Frontend Saved Views  
**Step:** 01  
**Date:** 2026-01-13  
**Tech Lead:** Jordan Rivera  
**AI Agent:** Development Team Agent (Claude 3.5 Sonnet)  
**Quality Gate Level:** Level 2 — Code Quality

---

## Context

This is the first step in the Saved Views feature. Before the frontend can store or retrieve SavedViews, the backend must provide a persistence layer and a REST API. This step produces that foundation.

## Scope

### In Scope

- Database migration to create the `saved_views` table
- REST API endpoints: `GET /api/saved-views`, `POST /api/saved-views`, `PATCH /api/saved-views/:id`, `DELETE /api/saved-views/:id`
- Request validation (name max 100 chars, max 50 views per user per listViewId)
- Response types (TypeScript interfaces shared between backend and frontend)
- Unit tests for the API handlers

### Out of Scope

- Frontend code of any kind
- Sharing SavedViews between users
- Any list view-specific logic beyond storing the `listViewId` field

## Inputs

| Input | Location |
|---|---|
| PRODUCT.md | examples/frontend-saved-views/PRODUCT.md |
| ARCHITECTURE.md | examples/frontend-saved-views/ARCHITECTURE.md |
| Data model | ARCHITECTURE.md — Data Model section |
| Existing API conventions | ARCHITECTURE.md — Patterns and Conventions section |

## Expected Outputs

| Artefact | Description |
|---|---|
| `migrations/YYYYMMDD_create_saved_views.sql` | Database migration |
| `src/api/saved-views/routes.ts` | Route handlers |
| `src/api/saved-views/validators.ts` | Input validation |
| `src/types/saved-view.ts` | Shared TypeScript types |
| `src/api/saved-views/routes.test.ts` | Unit tests |

## Acceptance Criteria

- [ ] The migration creates the `saved_views` table with all fields from the data model
- [ ] `GET /api/saved-views?listViewId=X` returns only the authenticated user's views for the specified list view
- [ ] `POST /api/saved-views` creates a SavedView; rejects if name > 100 chars or user already has 50 views for that listViewId
- [ ] `PATCH /api/saved-views/:id` updates name and/or isPinned; rejects if the view does not belong to the authenticated user
- [ ] `DELETE /api/saved-views/:id` deletes the view; rejects if the view does not belong to the authenticated user
- [ ] `userId` is always set from the session, never from the request body
- [ ] All handlers have unit tests covering happy path and key error cases

## Prompt

```
## Architecture
[SavedView data model and API conventions from ARCHITECTURE.md]

## Domain Language
- SavedView: a user-defined configuration of filters and column visibility saved for reuse on a specific list view
- pin: the action of marking a SavedView as always visible at the top of the sidebar
- restore: the action of applying a SavedView's saved filter and column configuration to the current list view
- listViewId: the identifier of the list view a SavedView belongs to

## Task
Implement Step 01 of the Saved Views feature: the database migration and REST API.

Produce:
1. A SQL migration file creating the `saved_views` table
2. TypeScript route handlers for GET, POST, PATCH, DELETE on /api/saved-views
3. Input validation (name max 100 chars, max 50 views per user per listViewId)
4. Shared TypeScript interfaces for SavedView request/response types
5. Unit tests for each handler covering happy path and key error cases

Constraints:
- userId must always be taken from the authenticated session, never from the request body
- Follow the existing route handler and validation patterns described in ARCHITECTURE.md
- Use domain language terms throughout

Ask clarifying questions if anything is ambiguous.
```

## Notes

- The existing API uses Express-style route handlers. Follow the same pattern.
- The `filters` and `columns` fields are stored as JSONB in PostgreSQL.
- Unit tests use the existing Vitest + Supertest setup.
