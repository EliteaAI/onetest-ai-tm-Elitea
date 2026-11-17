---
id: ELITEA-4720
title: "Pipeline — Test Pipeline Panel Controls and Session Behavior"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7155]
---

# ELITEA-4720: Pipeline — Test Pipeline Panel Controls and Session Behavior

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the Test Pipeline panel opens on demand, runs the pipeline, exposes the Context, Run History and Clear chat controls, blocks sending while there are unsaved changes, keeps a run going when closed, and remembers its width.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- A saved, fully configured pipeline exists (e.g. "LLM 1" (LLM, entry point) → End) whose run takes a few seconds.

---

## Test Data

| Field | Value |
|-------|-------|
| Message 1 | `Hello` |
| Message 2 | `Write a short poem about pipelines` |
| Unsaved edit | change the pipeline Description |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline | The Test panel is closed; the canvas takes the full width; the "Test Pipeline" button is enabled |
| 2 | Click "Test Pipeline" | The Test panel opens on the right with the message input and model selector; the "Test Pipeline" button is replaced by the panel controls |
| 3 | Send `Hello` | The user message and the pipeline response appear in the panel; the active node is highlighted on the canvas during the run |
| 4 | Check the Context icon in the panel controls | It shows a percentage (e.g. "1%") |
| 5 | Click the Context icon | A popover opens showing tokens, messages and summaries, and an "Edit" action |
| 6 | Close the popover; hover the Run History icon; click it | Tooltip "Run History"; Run History opens and lists the run |
| 7 | Return to the panel; change the pipeline Description (do not save); close the panel ("✕") | The "Test Pipeline" button is shown and stays ENABLED despite the unsaved change |
| 7a | Click "Test Pipeline" to reopen the panel | The panel opens with the same conversation |
| 8 | Type a message and hover the send button | Hint "Save the pipeline to test the latest changes." is shown and sending is blocked |
| 9 | Click "Save"; send `Hello` again | The message is sent and a response appears |
| 10 | Send `Write a short poem about pipelines`; while it is running click the panel "✕" | The panel closes; the "Test Pipeline" button is shown again; the canvas still highlights the running node |
| 11 | Click "Test Pipeline" again | The same conversation is shown, with the run's progress / completed response |
| 12 | Drag the handle between the canvas and the panel to make the panel wider; reload the page; open the Test panel | The panel opens with the widened width |
| 13 | Click the Clear chat icon | All messages are removed from the panel |

---

## Expected Final State

The Test panel works as an on-demand side panel: runs, context info, history, clear chat and resize behave as specified; unsaved changes block sending with the save hint; closing the panel does not stop a run.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Sending is blocked only while there are unsaved changes, with the hint shown.
- The run continues after closing the panel; width persists after reload; Clear chat empties the conversation.

**Fail:**
- The panel is open by default, or controls are missing.
- Sending succeeds with unsaved changes, or no hint is shown.
- Closing the panel stops the run or loses the conversation; width is not remembered.
