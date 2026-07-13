---
id: ELITEA-1960
title: "Remote MCP — Cancel During Creation"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1960: Remote MCP — Cancel During Creation

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that cancelling during MCP creation shows a confirmation dialog, and that confirming cancellation navigates away without creating the MCP.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has navigated to the MCP creation page and selected "Remote MCP".

---

## Test Data

| Field | Value |
|-------|-------|
| Toolkit Name | autotest_cancelled |
| URL | https://mcp.example.com/sse |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to MCP creation page and select "Remote MCP" | Form page loads |
| 2 | Fill "Toolkit Name *" with "autotest_cancelled" | Field accepts and displays the input |
| 3 | Fill "Url *" with "https://mcp.example.com/sse" | Field accepts and displays the URL |
| 4 | Click "Cancel" button (instead of Save) | Cancel action is triggered |
| 5 | Verify a warning confirmation dialog appears asking to confirm cancellation | Confirmation dialog is displayed |
| 6 | Click "Discard" to confirm cancellation | Cancellation is confirmed |
| 7 | Verify navigation goes back to MCP create page | User is navigated away from the creation form |
| 8 | Verify "autotest_cancelled" does NOT appear in MCP list | MCP is absent from the list |

---

## Expected Final State

No MCP with the name "autotest_cancelled" is created; the MCP list does not contain it after cancellation.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Confirmation dialog appears on Cancel; MCP is not created after Discard.

**Fail:**
- Any step produces an error or unexpected result.
- No confirmation dialog appears, or MCP is created despite cancellation.
