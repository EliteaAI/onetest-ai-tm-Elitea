---
id: ELITEA-2913
title: "Viewer Role — Restricted Actions Hidden, Disabled, or Blocked"
priority: high
type: functional
module: toolkits-indexes
status: draft
execution_type: manual
tags: [feat:toolkit-redesign, permissions, viewer-role]
requirements: []
---
# ELITEA-2913: Viewer Role — Restricted Actions Hidden, Disabled, or Blocked

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify a user with the Viewer role cannot access "+ Index" (including via direct URL navigation), "Delete Index", "Stop", or "Reindex", while read-only pages remain accessible.

**Coverage:**
- "+ Index" hidden or disabled on the Toolkit details page
- Direct URL navigation to the New Index page is restricted for Viewer (does not present a functional index-creation form)
- "Delete Index" hidden or disabled on the Index details page
- "Stop"/"Reindex" hidden or disabled on Activity and Configuration
- "Search" and "Run History" remain accessible and functional

## Preconditions

- A user account with the Viewer role, with access to a project containing an existing Index
- Logged in to {{base_url}} as that Viewer-role user
- The exact URL of the New Index page for a toolkit accessible to this Viewer (obtained beforehand, e.g., from an Editor-role session)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with an existing Index accessible to the Viewer account |
| New Index URL | The New Index page URL for that toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Toolkit details page as the Viewer-role user. | Page displays. |
| 2 | Inspect "+ Index". | "+ Index" is hidden or disabled. |
| 3 | Enter the New Index page URL for this toolkit directly into the browser address bar and navigate to it. | Access is restricted — the Viewer is redirected away, shown an access-restricted message, or otherwise not presented with a functional index-creation form. |
| 4 | Open an existing Index's details page. | Page displays. |
| 5 | Inspect "Delete Index". | "Delete Index" is hidden or disabled. |
| 6 | Click "Activity". | "Activity" tab displays. |
| 7 | Inspect "Stop" and "Reindex". | Both are hidden or disabled. |
| 8 | Click "Configuration". | "Configuration" tab displays with fields visible. |
| 9 | Inspect "Stop" and "Reindex" on "Configuration". | Both are hidden or disabled. |
| 10 | Click "Search". | Search page opens and a search can be executed. |
| 11 | Click "Run History". | Run History page opens and displays existing records. |

## Expected Final State

Viewer can view Configuration, Activity, Search, and Run History, but cannot trigger any create/delete/stop/reindex action, including via direct URL navigation to the New Index page.

## Pass/Fail Criteria

**Pass:**
- All restricted actions (including direct URL access to New Index) are hidden, disabled, or blocked for Viewer
- "Search" and "Run History" remain fully functional for Viewer

**Fail:**
- Any restricted action is available/clickable for Viewer
- Direct URL navigation presents a functional New Index creation form to Viewer
- "Search" or "Run History" is unexpectedly blocked for Viewer
