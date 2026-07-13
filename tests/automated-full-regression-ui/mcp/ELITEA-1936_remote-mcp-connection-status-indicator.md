---
id: ELITEA-1936
title: "Remote MCP — Connection Status Indicator"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1936: Remote MCP — Connection Status Indicator

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the connection status indicator is displayed on Remote MCP cards in the list and on the detail page, and that triggering authentication updates the status to "Connected".

---

## Preconditions

- User is logged in to the Elitea platform.
- At least one Remote MCP exists in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP list page | MCP list loads |
| 2 | Verify each Remote MCP card displays connection status badge (shows "Disconnected" with icon) | All Remote MCP cards show "Disconnected" badge |
| 3 | Open a Remote MCP detail page | Detail page loads |
| 4 | Verify connection status area shows "Not Connected" with a "Login" button | Status area displays correctly |
| 5 | Click "Login" button | Authentication/connection flow initiates |
| 6 | Verify authentication/connection flow initiates | Login flow or redirect appears |
| 7 | Verify status changes to "Connected" upon successful authentication | Status updates to "Connected" |

---

## Expected Final State

The Remote MCP shows "Connected" status after a successful authentication flow is completed.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Connection status updates to "Connected" after successful login.

**Fail:**
- Any step produces an error or unexpected result.
- Status does not update after authentication, or Login button is missing.
