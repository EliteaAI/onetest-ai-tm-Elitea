---
id: ELITEA-2419
title: "Copy assistant response to clipboard"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-2419: Copy assistant response to clipboard

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that Copy assistant response to clipboard. Success is confirmed when paste the clipboard content into an external text field (or the widget input) — verify it matches the assistant response text.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant widget | Target page/section loads successfully. |
| 2 | Send the message "Explain in one sentence what an AI agent is" | Action completes without error and produces the expected UI state. |
| 3 | Wait for the assistant response to appear | Wait completes; subsequent state is ready. |
| 4 | Locate the "Copy to clipboard" button on the assistant's response bubble | Action completes without error and produces the expected UI state. |
| 5 | Click the "Copy to clipboard" button — verify a visual confirmation (e.g., icon change, tooltip "Copied") appears | Control responds; expected next state is shown. |
| 6 | Paste the clipboard content into an external text field (or the widget input) — verify it matches the assistant response text | Field accepts the input and displays the entered value. |

---

## Expected Final State

Paste the clipboard content into an external text field (or the widget input) — verify it matches the assistant response text.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Copy assistant response to clipboard.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
