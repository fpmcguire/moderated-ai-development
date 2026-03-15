# Architecture

**Project:** Frontend Saved Views  
**Date:** 2026-01-12  
**Tech Lead:** Jordan Rivera

---

## Overview

The Saved Views feature is implemented entirely on the frontend as a React feature module. SavedViews are persisted to the backend via a new REST API resource and surfaced in the UI through a sidebar panel. The feature integrates with the existing filter and column state management layer.

## Technology Stack

| Layer | Technology | Version | Rationale |
|---|---|---|---|
| Frontend | React | 18.x | Existing stack |
| State management | Zustand | 4.x | Existing store pattern |
| API client | React Query | 5.x | Existing data-fetching layer |
| Backend API | REST (JSON) | — | Existing API convention |
| Persistence | PostgreSQL | 15.x | Existing database |

## System Diagram

```
[List View Page]
      │
      ├──► [Filter State] ──┐
      │                     ├──► [SavedView Store (Zustand)]
      └──► [Column State] ──┘              │
                                           ├──► [SavedViews API Client (React Query)]
                                           │              │
                                  [Sidebar Panel]         ▼
                                                  [Backend REST API]
                                                          │
                                                          ▼
                                                   [PostgreSQL]
```

## Key Design Decisions

### Decision 1: Store SavedView state in Zustand alongside filter and column state

**Context:** The existing filter and column state is managed in a Zustand store. SavedViews need to read and write this state.  
**Decision:** Add a `savedViews` slice to the existing Zustand store rather than creating a separate store.  
**Rationale:** Keeps all list view state co-located, simplifies save/restore logic, and avoids store synchronisation complexity.  
**Consequences:** The Zustand store becomes slightly larger. Care must be taken not to couple the SavedView slice to view-specific state that should remain local.

### Decision 2: Sidebar panel as the primary SavedView management surface

**Context:** SavedViews need a persistent, discoverable location in the UI.  
**Decision:** Add a collapsible sidebar panel to list view pages, housing the SavedView list and management actions.  
**Rationale:** Sidebars are a conventional location for saved configurations in data tools. Collapsible keeps screen real estate available for the list itself.  
**Consequences:** Requires a sidebar layout refactor for list view pages. Product Owner has approved this.

---

## Data Model

```
SavedView {
  id: UUID
  userId: UUID
  name: string (max 100 chars)
  listViewId: string         // identifies which list view this applies to
  filters: FilterState       // serialised filter configuration
  columns: ColumnState       // serialised column visibility/order
  isPinned: boolean
  createdAt: timestamp
  updatedAt: timestamp
}
```

## Integration Points

| Integration | Direction | Protocol | Notes |
|---|---|---|---|
| SavedViews REST API | Frontend → Backend | JSON over HTTPS | New resource: `/api/saved-views` |
| Filter state (Zustand) | Read/write | In-process | Existing store slice |
| Column state (Zustand) | Read/write | In-process | Existing store slice |

## Security Considerations

- SavedViews are scoped to the authenticated user via the session token — users cannot read each other's views
- The `userId` is set server-side from the session; it is never trusted from the client request body
- SavedView names are sanitised before display to prevent XSS

## Performance Considerations

- SavedViews are fetched once on sidebar open and cached by React Query
- Restoring a SavedView writes to the Zustand store synchronously — no async latency on the restore action

## Constraints

- Maximum 50 SavedViews per user per list view (enforced server-side)
- SavedView names must be unique per user per list view

## Patterns and Conventions

- Follow the existing Zustand slice pattern: `src/stores/savedViewsSlice.ts`
- Follow the existing React Query hook pattern: `src/hooks/useSavedViews.ts`
- All new components in `src/features/saved-views/`
- Use domain language terms throughout — see DOMAIN_LANGUAGE_MATRIX.md equivalent in PRODUCT.md
