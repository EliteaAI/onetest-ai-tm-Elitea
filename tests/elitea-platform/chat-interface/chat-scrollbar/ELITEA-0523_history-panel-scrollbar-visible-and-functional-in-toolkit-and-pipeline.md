---
id: ELITEA-0523
title: "History panel — scrollbar visible and functional in Toolkit and Pipeline history panels when list overflows"
priority: medium
type: functional
module: chat-scrollbar
status: ready
execution_type: manual
tags: [feat:toolkits, issue:3704, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3704]
---
# ELITEA-0523: History panel — scrollbar visible and functional in Toolkit and Pipeline history panels when list overflows

**Module:** Chat Scrollbar · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the history panel — accessible via the history (clock) icon in Toolkit Test Settings and Pipeline chat — has a working scrollbar when the conversation history list overflows the panel height.

**Coverage:**
- History icon opens a history/conversation panel in Toolkit and Pipeline contexts
- Scrollbar appears in the history panel when the list of history entries overflows
- Scrollbar is draggable and mouse wheel scrolling works within the history panel
- Full history list is reachable

## Preconditions

- Logged in to {{base_url}} with Editor or Admin role
- A Toolkit with multiple prior test runs (to populate the history panel)
- A Pipeline with multiple prior executions (to populate the Pipeline history panel)
- History panel accessible via the clock/history icon in both contexts
- Chrome or Edge, latest stable

## Test Data

- Toolkit with 10+ prior test run history entries
- Pipeline with 10+ prior execution history entries
- History panel icon: clock/history icon in the top-right toolbar of Toolkit and Pipeline pages

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits. Open a toolkit with many prior test runs. Click the history (clock) icon in the top-right area of the page. | History panel opens showing a list of past test run conversations. |
| 2 | If needed, perform multiple tool test runs to ensure the history list is long enough to overflow the panel. Then reopen the history panel. | History list contains enough entries to overflow the panel height. |
| 3 | Observe the right edge of the history panel. | A scrollbar is visible when the history list overflows. |
| 4 | Drag the scrollbar thumb and use the mouse wheel to scroll the history list. | History list scrolls correctly via both methods; all entries are reachable. |
| 5 | Navigate to Pipelines. Open a Pipeline. Click the history (clock) icon. | Pipeline history panel opens with past run entries. |
| 6 | Ensure there are enough history entries to overflow the panel. Verify scrollbar appears and both drag and wheel scroll work. | Scrollbar present and functional in the Pipeline history panel. |

## Expected Final State

Scrollbar present and functional in the Pipeline history panel.

## Pass/Fail Criteria

**Pass:**
- History panel opens in both Toolkit and Pipeline contexts
- Scrollbar appears when history entries overflow the panel
- Dragging and wheel scrolling both work in the history panel

**Fail:**
- History panel has no scrollbar despite a long list of entries
- History panel entries below the fold unreachable
- Scrollbar visible but non-functional
