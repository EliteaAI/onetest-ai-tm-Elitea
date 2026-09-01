---
id: ELITEA-3073
title: "response_search and response_limit Tool-Args Fields Render Correctly in Light and Dark Theme"
priority: low
type: ui
module: openapi-toolkit-response-selection
status: draft
execution_type: manual
tags: [feat:toolkits, int:openapi, issue:6105, ui, theme]
requirements: [EliteaAI/elitea_issues#6105]
---

# ELITEA-3073: response_search/response_limit Fields Render Correctly Across Light/Dark Theme

**Module:** Toolkits & Credentials / OpenAPI Toolkit Response Selection · **Priority:** Low · **Type:** UI

**Objective:** Confirm the `response_search` and `response_limit` optional tool-argument fields (wherever surfaced in the UI — e.g. tool schema/args preview in an Agent or Chat tool-call view) render correctly, legibly, and without layout overlap in both light and dark theme.

---

## Preconditions

- A toolkit with an OpenAPI operation that supports `response_search`/`response_limit` is configured and its tool schema/args are visible somewhere in the UI (e.g. agent tool configuration, chat tool-call detail view).
- Access to toggle the application theme between light and dark.

---

## Test Data

| Field | Value |
|-------|-------|
| Theme | Light, Dark |

---

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | In light theme, navigate to the view surfacing the tool's args schema (including `response_search`/`response_limit`). | Both fields are visible, correctly labeled, with legible contrast and no overlapping elements. |
| 2 | Switch to dark theme and revisit the same view. | Both fields remain visible and legible with correct dark-theme styling; no contrast or overlap regressions. |
| 3 | Resize the viewport (if applicable) in both themes. | No layout breakage/overlap at common breakpoints. |

---

## Expected Final State

The two new optional fields are visually consistent with the rest of the tool-args UI in both themes.

---

## Pass/Fail Criteria

**Pass:** Correct, legible, non-overlapping rendering in both light and dark theme.
**Fail:** Any contrast issue, overlap, truncation, or missing styling in either theme.

---

## Notes

Carried over from the original #6105 checklist; not exercised live this session (live session focused on API-level behavior). Execute once the fields are confirmed visible in a specific UI surface.
