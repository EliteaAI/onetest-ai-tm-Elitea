---
id: ELITEA-1939
title: "Remote MCP — Test Settings — Fullscreen Mode"
priority: medium
type: functional
module: elitea-platform
status: draft
execution_type: automated
tags: [automated:UI:regression]
requirements: []
---

# ELITEA-1939: Remote MCP — Test Settings — Fullscreen Mode

**Module:** elitea-platform · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Test Settings panel can be toggled into fullscreen mode and back, and that tool selection and chat functionality remain operational in fullscreen.

---

## Preconditions

- User is logged in to the Elitea platform.
- A Remote MCP detail page with Test Settings panel is open.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a Remote MCP detail page with Test Settings panel visible | Detail page loads with Test Settings panel |
| 2 | Click "Fullscreen mode" button in test panel header | Test panel expands to fullscreen view |
| 3 | Verify test panel expands to fullscreen view | Panel occupies the full screen |
| 4 | Verify tool selection and chat area remain functional in fullscreen | Tool dropdown and chat area are usable |
| 5 | Click fullscreen toggle button again | Fullscreen mode is exited |
| 6 | Verify panel returns to normal split-pane size | Panel returns to standard layout |

---

## Expected Final State

The Test Settings panel returns to normal split-pane layout after toggling fullscreen mode off.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Fullscreen toggle works in both directions and functionality is preserved.

**Fail:**
- Any step produces an error or unexpected result.
- Panel does not expand or collapse correctly, or functionality is broken in fullscreen.
