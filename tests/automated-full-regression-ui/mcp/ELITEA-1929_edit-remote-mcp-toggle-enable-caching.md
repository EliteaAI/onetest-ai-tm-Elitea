---
id: ELITEA-1929
title: "Edit Remote MCP — Toggle Enable Caching"
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: automated
tags: [automated:UI:regression]
requirements: []
automation_test_id: tests.ui.toolkits.test_mcp_edit_toggle_enable_caching.test_mcp_edit_toggle_enable_caching
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/548
---

# ELITEA-1929: Edit Remote MCP — Toggle Enable Caching

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the "Enable Caching" toggle on a Remote MCP can be turned off and back on, with the change persisted in both Form and Raw JSON views after reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.
- "Enable Caching" is checked by default.

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
| 2 | Note current state of "Enable Caching" checkbox (checked by default) | Checkbox is checked |
| 3 | Click "Enable Caching" to uncheck it | Checkbox becomes unchecked |
| 4 | Click Save | Operation completes successfully |
| 5 | Reload page — verify "Enable Caching" is unchecked | Checkbox remains unchecked after reload |
| 6 | Switch to Raw Json — verify "enable_caching": false in JSON | JSON shows enable_caching as false |
| 7 | Re-enable caching and save again | Checkbox is checked and saved |

---

## Expected Final State

The "Enable Caching" toggle state is persisted correctly and reflected in the Raw JSON view; the setting is restored to enabled after cleanup.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Enable Caching state is persisted and reflected correctly in Raw JSON.

**Fail:**
- Any step produces an error or unexpected result.
- Toggle state is not persisted or Raw JSON does not reflect the change.
