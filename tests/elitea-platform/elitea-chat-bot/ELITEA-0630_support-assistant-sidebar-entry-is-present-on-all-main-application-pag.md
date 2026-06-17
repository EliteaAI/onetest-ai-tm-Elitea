---
id: ELITEA-0630
title: "Support Assistant sidebar entry is present on all main application pages without disrupting layout"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [persistence, regression, cross-page, layout]
requirements: [#4780, #4774]
---
# ELITEA-0630: Support Assistant sidebar entry is present on all main application pages without disrupting layout

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** The Support Assistant entry must appear consistently across every main section of the application, and its presence must not push other nav items out of view, cause layout shifts, or affect the main content area on any page.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant feature is enabled
User has access to Chat, Agents, Pipelines, Credentials, Toolkits, Artifacts, and Settings

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Chat page. Inspect the bottom of the sidebar. | Support Assistant entry is visible at the bottom of the sidebar. All standard nav items above it are fully visible and clickable. Main content area has normal width. |
| 2 | Click on Agents in the sidebar to navigate to the Agents page. | Agents page loads. Support Assistant entry is still present at the sidebar bottom. Page layout is intact. |
| 3 | Navigate to Pipelines, then Credentials, then Toolkits in sequence. | On each page: Support Assistant entry visible, all standard nav items accessible, main content area unaffected. |
| 4 | Navigate to Artifacts, then Settings. | Same as above — entry present, layout intact. |
| 5 | On any of these pages, collapse the sidebar and verify the layout in collapsed mode. | Collapsed sidebar shows correct icons for all items. Support Assistant entry has an icon (not an invisible block). Main content area expands correctly in collapsed mode. |

## Expected Final State

Collapsed sidebar shows correct icons for all items. Support Assistant entry has an icon (not an invisible block). Main content area expands correctly in collapsed mode.

## Pass/Fail Criteria

Pass: Support Assistant entry present on every listed page; All standard nav items are accessible on every page; Main content layout is unchanged on every page; Collapsed sidebar shows a visible Support Assistant icon.
Fail: Support Assistant entry missing on one or more pages; Any standard nav item hidden or inaccessible due to the Support Assistant entry; Main content area layout disrupted on any page; Collapsed sidebar shows an empty/invisible click target instead of an icon.
