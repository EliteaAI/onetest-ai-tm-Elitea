---
id: ELITEA-2005
title: "Entry Point Node — Trigger Types (Chat Message, Webhook)"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_entry_point_trigger_types_persist.test_entry_point_trigger_types_persist
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2005: Entry Point Node — Trigger Types (Chat Message, Webhook)

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that the entry point node exposes the two selectable trigger types (Chat Message, Webhook; Schedule was removed from the Trigger select by EL-7011) and that selecting each trigger type persists correctly after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline exists with a single entry point node (no HITL/Printer/interrupts).

---

## Test Data

| Field | Value |
|-------|-------|
| Trigger options | Chat Message, Webhook |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline with a single entry point node (no HITL/Printer/interrupts) | Pipeline is created with one node |
| 2 | Click on the entry point node (opens its side panel) — locate "Trigger" dropdown (shows "Chat Message" by default) | Trigger dropdown is visible and defaults to "Chat Message" |
| 3 | Open Trigger dropdown — verify 2 options appear: "Chat Message", "Webhook" | Both options are listed in the dropdown (no Schedule) |
| 4 | Select and Apply "Webhook" — verify dropdown updates to "Webhook" with default webhook settings | Dropdown shows "Webhook" and webhook settings appear |
| 5 | Save pipeline — reload — verify Trigger shows "Webhook" | Webhook trigger is persisted after reload |
| 6 | Switch back to "Chat Message" | Dropdown returns to "Chat Message" |
| 7 | Repeat with a different node type as entry point (e.g., Code node) — verify Trigger dropdown still appears with both options | Both trigger types are available regardless of entry point node type |

---

## Expected Final State

The entry point node supports both selectable trigger types (Chat Message, Webhook), each persists after save/reload, and the trigger dropdown is available for any node type used as entry point.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Both trigger types (Chat Message, Webhook) are selectable and persist correctly after save and reload.

**Fail:**
- Any step produces an error or unexpected result.
- A trigger type is missing, or the selected trigger does not persist after saving.
