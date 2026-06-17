---
id: ELITEA-0609
title: "Collapsed sidebar shows Support Assistant icon entry — not an invisible click area"
priority: medium
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [collapsed-sidebar, discoverability, story:4780, r-2.0.3, icon]
requirements: [4780]
---
# ELITEA-0609: Collapsed sidebar shows Support Assistant icon entry — not an invisible click area

**Module:** Elitea Chat Bot · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when the sidebar is collapsed to icon-only mode, the Support Assistant entry is represented by a visible icon — not an empty or invisible area. In collapsed sidebar mode, icons are the only navigation affordance. An invisible entry makes the feature undiscoverable for keyboard-first and space-efficient users.

## Preconditions

Support Assistant is enabled and the sidebar entry is visible.
Tester is on a page with the full sidebar available (e.g., Chat or Agents page).

## Test Data

None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the sidebar is in expanded mode (text labels visible) | Sidebar shows both icons and text labels for all entries including Support Assistant |
| 2 | Collapse the sidebar (click the collapse/minimize button on the sidebar) | Sidebar collapses to icon-only mode |
| 3 | Locate the Support Assistant entry area in the collapsed sidebar | A visible icon representing the Support Assistant is present — it is NOT an empty or invisible click region |
| 4 | Hover over the icon | A tooltip appears with the label (e.g., "Support Assistant" or "Support") |
| 5 | Click the icon in collapsed sidebar mode | The Support Assistant panel opens correctly |

## Expected Final State

The Support Assistant panel opens correctly

## Pass/Fail Criteria

PASS: Visible icon present in collapsed sidebar; tooltip on hover; panel opens on click.
FAIL: No visible icon in collapsed sidebar; invisible click area; tooltip missing.
