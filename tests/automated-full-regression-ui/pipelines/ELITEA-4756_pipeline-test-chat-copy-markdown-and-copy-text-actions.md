---
id: ELITEA-4756
title: "Regression - Pipeline test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast"
priority: critical
type: regression
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_test_chat_copy_icons.test_pipeline_test_chat_copy_icons_show_tooltip_and_toast
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/24c60ce64ea0c4198d62f840a2e7b96119d7a637
tags: [feat:chat, feat:pipelines, r-2.0.9, automated:UI:regression]
requirements: ["EliteaAI/elitea_issues#5838"]
---

# ELITEA-4756: Regression - Pipeline test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast

**Module:** pipelines · **Priority:** critical · **Type:** regression

**Objective:** Pipeline test chat: Copy markdown and Copy text icons are visible, clickable and confirmed by a toast.

Manual source: ELITEA-4750

---

## Preconditions

- User is logged in to {{base_url}} in a project where they can edit entities (e.g. **Bugs & Features**).
- A pipeline exists with at least one LLM node connected to End (e.g. **Story taller**).

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline | any pipeline with an LLM node, e.g. Story taller |
| Input | any text, e.g. `go` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open **Pipelines** in the left menu and open the pipeline | Pipeline editor opens in **Flow** view; **Test Pipeline** button is visible. |
| 2 | Click **Test Pipeline** | Test chat panel opens on the right with an input box. |
| 3 | Enter the input from Test Data and click the send arrow | Pipeline runs (**Run 1 details** appears) and the final response is shown in the chat. |
| 4 | Observe the icons below the pipeline response | **Copy markdown** (M icon) and **Copy text** (copy icon) are visible. |
| 5 | Hover the **M** icon in the pipeline response toolbar | Tooltip **Copy markdown** is shown. |
| 6 | Click **Copy markdown** | Icon is clickable; confirmation toast **Markdown copied to clipboard.** appears. |
| 7 | Hover the copy icon next to it in the pipeline response toolbar | Tooltip **Copy text** is shown. |
| 8 | Click **Copy text** | Icon is clickable; confirmation toast **Text copied to clipboard.** appears. |

---

## Expected Final State

Copy markdown and Copy text icons are available under the pipeline response and each click is confirmed by a toast.

---

## Pass/Fail Criteria

**Pass:**
- **Copy markdown** and **Copy text** icons are visible and clickable.
- After each click a confirmation toast appears.

**Fail:**
- Either icon is missing or not clickable.
- No confirmation toast appears after clicking.
