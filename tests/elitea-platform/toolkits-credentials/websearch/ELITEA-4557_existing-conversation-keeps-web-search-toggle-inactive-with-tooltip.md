---
id: ELITEA-4557
title: "Existing conversation keeps Web Search toggle inactive with tooltip when later disabled"
priority: high
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- Web Search is available and can be enabled in a chat
- An admin can make Web Search unavailable afterward for that project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Tooltip text to verify | "Web Search is disabled by your administrator." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Web Search in a chat while it is available | Toggle shows ON |
| 2 | As an admin, make Web Search unavailable for that project (e.g. unset the shared toolkit in Settings → Web Search) | Setting saves |
| 3 | Return to the original chat | Web Search toggle is still visible (not removed) but rendered as inactive/disabled |
| 4 | Hover/inspect the toggle | Tooltip reads "Web Search is disabled by your administrator." |
| 5 | Send a message in this chat | No web search is attempted |

## Expected Final State

The chat retains the visual record of the toggle but cannot use it once Web Search becomes unavailable, with the correct disabled-state tooltip.

## Pass/Fail Criteria

**Pass:**
- Toggle remains visible, is inactive, shows the exact tooltip text, and no search occurs

**Fail:**
- Toggle disappears entirely, remains active, or shows incorrect/missing tooltip text
