---
id: ELITEA-4394
title: "Recent Runs STARTED link opens the correct run's own Analytics page with correct project context"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, issue:7033, r-2.0.8, agent-pipeline-analytics, recent-runs, navigation]
requirements: [EliteaAI/elitea_issues#7033]
---

# ELITEA-4394: Recent Runs STARTED link opens the correct run's own Analytics page with correct project context

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the STARTED timestamp of a run in the Recent Runs table navigates to that exact run's own Analytics detail page (resolved via the stable run identifier, with correct project context) — not the Agent/Pipeline editor and not a generic history page — for normal, error-status, and multi-model runs, that standard anchor behaviors (new tab, copy link) work, that back-navigation preserves the originating detail-view context, that access control is respected, and that legacy records with no navigable run identifier show plain text instead of a broken link.

**Coverage:**
- STARTED link resolves to the specific run's Analytics page (correct run data: cost, tokens, models)
- Works for normal-status, Error/failed-status, and multi-model runs
- Standard anchor behavior: open in new tab, copy link
- Back-navigation preserves originating date range and selected Agent/Pipeline
- Access-control: unavailable/not-found state for a user without access to that run
- Legacy run with no navigable identifier: timestamp is plain text, not a broken link

## Preconditions

- Logged in to `{{base_url}}`
- An Agent or Pipeline with: at least one normal-status run, at least one Error/failed-status run, and at least one multi-model run, all visible in Recent Runs
- A second user account without access to at least one specific run, if available
- A legacy run record with no navigable run identifier, if available in the test environment

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Entity | Agent or Pipeline with Recent Runs including normal, Error, and multi-model runs |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the detail view for the test Agent/Pipeline and locate the Recent Runs table | Table renders with STARTED, USER, VERSION, MODEL, TOTAL TOKENS, COST, STATUS columns; STARTED values are hyperlinks (except any legacy unlinked row) |
| 2 | Click the STARTED link of a normal-status run | Navigates to that specific run's own Analytics detail page; cost, tokens, and model data on that page match the clicked row |
| 3 | Return to the Recent Runs table and click the STARTED link of the Error/failed-status run | Link still works and opens that run's own Analytics page (not a generic error page) |
| 4 | Return to the Recent Runs table and click the STARTED link of the multi-model run | Opens that run's page; the page shows all models actually used in that run |
| 5 | Right-click (or long-press) a STARTED link and verify "open in new tab" and "copy link" are available and function as standard anchors | New tab opens the same run's page; copied link, when pasted/opened, resolves to the same run's page |
| 6 | From a run's Analytics page opened via STARTED link, use browser Back navigation | Returns to the originating Agent/Pipeline detail view with the same date range and entity selection preserved (not reset to defaults) |
| 7 | As a user without access to a specific run (if available), attempt to open that run's STARTED link | Standard unavailable/not-found state is shown, not a generic error or silent failure |
| 8 | If a legacy run record with no navigable run identifier is available, locate its row | STARTED timestamp displays as plain text (no link, no broken href) |

## Expected Final State

Every STARTED link in Recent Runs resolves to the exact corresponding run's own Analytics page with correct data and project context; standard browser link behaviors work; back-navigation preserves the originating view's context; access control and legacy-record handling behave per spec.

## Pass/Fail Criteria

**Pass:**
- Each STARTED link opens that specific run's own Analytics page with matching run data, for normal, Error, and multi-model runs
- New-tab and copy-link work as standard anchors
- Back-navigation preserves originating date range and entity selection
- Inaccessible run shows standard unavailable/not-found state
- Legacy run without identifier shows plain, unlinked text

**Fail:**
- Link opens the wrong run, the Agent/Pipeline editor, or a generic history page
- Error-status or multi-model run links are broken or show incomplete data
- New tab/copy link do not work as standard anchors
- Back-navigation resets date range or entity selection
- Inaccessible run throws an unhandled error or fails silently
- Legacy row shows a broken/dead link instead of plain text
