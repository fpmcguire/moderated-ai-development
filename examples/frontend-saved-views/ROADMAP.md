# Roadmap

**Project:** Frontend Saved Views  
**Date:** 2026-01-12  
**Owner:** Alex Chen

---

## Summary

The Saved Views feature is implemented in four steps. The first step establishes the data model and API. The second implements the Zustand store slice and React Query hooks. The third builds the sidebar panel UI. The fourth adds pinning and inline rename.

## Steps

| Step | Title | AI Agent | Status | Notes |
|---|---|---|---|---|
| STEP-01 | SavedView data model and REST API | Development Team (Claude) | Done | |
| STEP-02 | Zustand slice and React Query hooks | Development Team (Claude) | Done | |
| STEP-03 | Sidebar panel — list and restore | Development Team (Claude) | Planned | |
| STEP-04 | Pin and rename SavedViews | Development Team (Claude) | Planned | |

---

## Step Details

### STEP-01: SavedView data model and REST API

**Goal:** Define the SavedView database schema and implement the CRUD REST API endpoints.  
**Output:** Migration file, API route handlers, request/response types  
**AI Agent:** Development Team Agent (Claude)

### STEP-02: Zustand slice and React Query hooks

**Goal:** Implement the frontend state management and data-fetching layer for SavedViews.  
**Output:** `savedViewsSlice.ts`, `useSavedViews.ts` hook, type definitions  
**AI Agent:** Development Team Agent (Claude)

### STEP-03: Sidebar panel — list and restore

**Goal:** Build the sidebar panel UI that lists SavedViews and allows restore and delete.  
**Output:** `SavedViewsSidebar` component, `SavedViewItem` component, integration with list view pages  
**AI Agent:** Development Team Agent (Claude)

### STEP-04: Pin and rename SavedViews

**Goal:** Add the ability to pin a SavedView to the top of the sidebar and rename it inline.  
**Output:** Updated `SavedViewItem` with pin toggle and inline rename, updated API and store  
**AI Agent:** Development Team Agent (Claude)

---

## Milestones

| Milestone | Steps Included | Target Date | Status |
|---|---|---|---|
| Backend complete | STEP-01 | 2026-01-24 | Done |
| Frontend state complete | STEP-02 | 2026-01-31 | Done |
| UI complete | STEP-03, STEP-04 | 2026-02-14 | In Progress |

## Dependencies

- STEP-02 depends on STEP-01 (API must exist before hooks can be written)
- STEP-03 depends on STEP-02 (hooks must exist before UI can be built)
- STEP-04 depends on STEP-03 (sidebar must exist before pin/rename can be added)
