---
id: ELITEA-4703
title: "Test Pipeline Panel — Open/Close, Run, Controls, Resize and Session Behavior"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7155]
---
# ELITEA-4703: Test Pipeline Panel — Open/Close, Run, Controls, Resize and Session Behavior

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify the Test Pipeline panel in full: closed by default, opening/closing, running via message or chat starter, message actions, Run History / Context / Clear chat controls, resize and persistence, run continuation when closed, unsaved-changes blocking, and the on-canvas Run details chip.

**Coverage:**
- Closed by default, canvas full width
- Panel content: message input, model selector + settings, voice, attachments (module on), chat starters
- Running: response, thinking steps, message actions, active-node highlight
- Controls: Run History icon, Context icon (shown after conversation starts), Clear chat, ✕
- Resize (min/max), width remembered, canvas re-fit
- Closing mid-run keeps the run going
- Unsaved changes: button enabled, send blocked with hint on send-button hover
- On-canvas ⟲ and "Run N details" chip unchanged
- See ELITEA-4720 for the main flow

## Preconditions

- Logged in to {{base_url}}
- A saved, configured pipeline with an LLM node, two chat starters configured and the Attachments module ON

## Test Data

- Message: `Hello`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline. | Test panel is closed; canvas takes the full width. |
| 2 | Click **Test Pipeline**. | Panel opens with message input, model selector + ⚙ settings, voice input, attachments (paperclip), send button, and chat starters as chips. The Test Pipeline button is replaced by the panel controls. |
| 3 | Observe the controls before any message. | Run History icon present; **Context icon not shown yet**; Clear chat (broom) disabled. |
| 4 | Click a chat starter. | Pipeline runs; response and thinking steps (input/output per node) render; active node highlighted on the canvas. |
| 5 | Use message actions on the response: copy, regenerate, delete, listen. | All actions work. |
| 6 | Change the model via the model selector and ⚙ settings; send `Hello`. | The selected model/settings are used; response returned. |
| 7 | Use voice input. | Voice input is captured into the message input. |
| 8 | Attach a file via the paperclip and send. | Attachment is sent with the message. |
| 9 | Hover the **Run History** icon; click it. | Tooltip *"Run History"*; Run History opens. |
| 10 | Observe and hover the **Context** icon. | Shown as `◐ N%`; tooltip *"Context N% · Messages M · Summaries S"*. The old horizontal context bar is not present. |
| 11 | Click the Context icon; click **Edit**. | Popover with tokens used/limit, messages, summaries (clickable), and **Edit**; Edit opens the existing Context settings modal. |
| 12 | Continue the conversation until usage reaches warning and exceeded thresholds. | Context icon colour follows normal / warning / exceeded. |
| 13 | Start a run and click **Clear chat** while it is in progress. | The run is stopped and the chat is cleared; Clear chat becomes disabled. |
| 14 | Drag the handle between canvas and panel to the minimum and maximum. | Width is bounded (~320px min, ~50% of editor max); the canvas re-fits. |
| 15 | Reload the page and reopen the panel. | The chosen width is remembered. |
| 16 | Start a run, close the panel with ✕ mid-run. | Test Pipeline button returns; the canvas keeps highlighting the active node; the run continues. |
| 17 | Reopen the panel. | Same conversation and progress are shown. |
| 18 | Observe the on-canvas ⟲ history icon and "Run N details" chip with the panel open and closed. | Progress, stop and View details work as before in both states. |
| 19 | Edit any pipeline field without saving; open the panel. | Test Pipeline button stays enabled; hovering the send button shows *"Save the pipeline to test the latest changes."* and sending is blocked. |
| 20 | Save; send a message. | Sending works again. |
| 21 | Compare the open panel with the Figma frame "Create new_Default" (Test panel open). | UI matches. |

## Expected Final State

The Test panel opens only on demand, runs the pipeline with full message tooling, its controls work as specified, width persists per user, runs continue when the panel is closed, and unsaved changes block sending with the save hint.

## Pass/Fail Criteria

**Pass:**
- Closed by default; opens/closes correctly
- Runs via chat starter and message; actions, model, voice, attachments work
- Run History, Context (after conversation starts), Clear chat behave as specified
- Resize bounded and remembered; run continues when closed
- Unsaved changes block sending with the exact hint

**Fail:**
- Panel open by default or does not close
- Any control missing/misbehaving; old context bar still present
- Closing the panel stops the run or clears the conversation
- Sending allowed with unsaved changes
