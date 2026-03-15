# Product Definition

**Project:** Frontend Saved Views  
**Description:** Allow users to save, name, and reuse filter and column configurations on list views  
**Date:** 2026-01-10  
**Owner:** Alex Chen

---

## Problem Statement

Users frequently configure the same filter combinations and column layouts to perform their daily work. Each time they return to a list view, these settings are lost and must be re-applied manually. This costs time, introduces error, and reduces confidence in the tool.

## Target Users

| User | Context | Goal |
|---|---|---|
| Daily analyst | Reviews a specific filtered list every morning | Save their standard filter as a named view and open it in one click |
| Team lead | Needs the same subset of columns shared across the team | Create a shared view the whole team can access |
| Power user | Works across multiple filtered contexts in a day | Switch between named views rapidly without losing any configuration |

## Goals

1. Users can save a named configuration of filters and column visibility for any list view
2. Users can restore a saved view in one click
3. Users can manage (rename, delete, pin) their saved views
4. Team leads can share saved views with their team

## Non-Goals

- Saved views will not support scheduled reports or data exports in this phase
- Saved views will not be nested or hierarchical
- Admin management of all users' saved views is out of scope

## High-Level Requirements

| # | Requirement | Priority |
|---|---|---|
| 1 | Create a SavedView from the current filter and column state | Must have |
| 2 | Name a SavedView at creation time | Must have |
| 3 | Restore a SavedView by selecting it from a list | Must have |
| 4 | Delete a SavedView | Must have |
| 5 | Rename a SavedView | Should have |
| 6 | Pin a SavedView to the top of the list | Should have |
| 7 | Share a SavedView with teammates | Nice to have |

## Acceptance Criteria

- [ ] A user can create a SavedView from any list view
- [ ] A user can see all their SavedViews in a sidebar panel
- [ ] Selecting a SavedView applies its filters and columns immediately
- [ ] A user can delete a SavedView with confirmation
- [ ] A user can rename a SavedView inline
- [ ] Pinned SavedViews appear at the top of the sidebar panel

## Assumptions and Constraints

- SavedViews are stored per-user; sharing is a later phase
- The existing filter and column APIs expose the state needed to serialise a SavedView
- The frontend is a React SPA; no server-side rendering is involved

## Open Questions

| Question | Owner | Due |
|---|---|---|
| What is the maximum number of SavedViews per user? | Alex Chen | 2026-01-15 |
| Should pinning be per-user or per-team? | Alex Chen | 2026-01-15 |
