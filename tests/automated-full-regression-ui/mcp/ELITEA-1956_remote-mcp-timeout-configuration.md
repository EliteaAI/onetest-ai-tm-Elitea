---
id: ELITEA-1956
title: "Remote MCP — Timeout Configuration"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1956: Remote MCP — Timeout Configuration

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Timeout field on a Remote MCP can be changed from its default value, saved, and that the new value is persisted in both the Form view and the Raw JSON.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.

---

## Test Data

| Field | Value |
|-------|-------|
| Default Timeout | 300 |
| New Timeout | 60 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Locate "Timeout" field — verify default value is 300 | Field shows 300 |
| 3 | Verify info icon (tooltip) is present next to "Timeout" label | Info icon is visible |
| 4 | Change timeout to 60 | Field displays 60 |
| 5 | Save MCP | Operation completes successfully |
| 6 | Reload page — verify timeout shows 60 | Timeout field shows 60 after reload |
| 7 | Switch to Raw Json — verify "timeout": 60 in settings | JSON shows timeout as 60 |
| 8 | Change back to 300 and save | Timeout is restored to default |

---

## Expected Final State

The Timeout value is updated, persisted, and confirmed in both Form and Raw JSON views; the value is restored to 300 after cleanup.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Timeout change is persisted and reflected in Raw JSON.

**Fail:**
- Any step produces an error or unexpected result.
- Timeout value is not persisted or Raw JSON does not reflect the change.
