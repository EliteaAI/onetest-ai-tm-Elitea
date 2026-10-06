---
id: ELITEA-1931
title: "Edit Remote MCP — Modify Headers JSON"
priority: critical
type: functional
module: elitea-platform
status: draft
execution_type: manual
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1931: Edit Remote MCP — Modify Headers JSON

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Headers JSON editor on a Remote MCP accepts and persists custom headers, and that the saved values are visible after reload and in the Raw JSON view.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing Remote MCP is available and open on its detail page in Form view.

---

## Test Data

| Field | Value |
|-------|-------|
| Headers JSON | {"X-Custom-Header": "test-value"} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page in Form view | Detail page loads in Form view |
| 2 | Expand "Headers" section (click "Headers" accordion) | Headers accordion expands |
| 3 | Verify JSON editor for headers is visible (default: {}) | JSON editor shows empty object {} |
| 4 | Enter valid JSON: {"X-Custom-Header": "test-value"} | JSON editor accepts and displays the input |
| 5 | Click Save | Operation completes successfully |
| 6 | Reload page — expand Headers — verify JSON persisted | Headers JSON shows {"X-Custom-Header": "test-value"} |
| 7 | Switch to Raw Json view — verify headers appear in full JSON config | Full JSON includes the custom headers entry |

---

## Expected Final State

The custom header JSON is saved, persists after a page reload, and is visible in the full Raw JSON configuration.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Custom headers are saved and visible in both the Headers field and Raw JSON view.

**Fail:**
- Any step produces an error or unexpected result.
- Headers are not persisted or not reflected in the Raw JSON.
