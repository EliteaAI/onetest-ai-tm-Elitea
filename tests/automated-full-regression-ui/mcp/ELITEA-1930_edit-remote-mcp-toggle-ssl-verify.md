---
id: ELITEA-1930
title: "Edit Remote MCP — Toggle SSL Verify"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1930: Edit Remote MCP — Toggle SSL Verify

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Ssl Verify" toggle on a Remote MCP can be turned off, and that the change is persisted in both Form and Raw JSON views after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.
- "Ssl Verify" is checked by default.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Note current state of "Ssl Verify" checkbox (checked by default) | Checkbox is checked |
| 3 | Click "Ssl Verify" to uncheck it | Checkbox becomes unchecked |
| 4 | Click Save | Operation completes successfully |
| 5 | Reload page — verify "Ssl Verify" is unchecked | Checkbox remains unchecked after reload |
| 6 | Switch to Raw Json — verify "ssl_verify": false in JSON | JSON shows ssl_verify as false |

---

## Expected Final State

The "Ssl Verify" toggle is unchecked, saved, and reflected in the Raw JSON view after a page reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Ssl Verify state is persisted and shown correctly in Raw JSON.

**Fail:**
- Any step produces an error or unexpected result.
- Toggle state is not persisted or Raw JSON does not reflect the change.
