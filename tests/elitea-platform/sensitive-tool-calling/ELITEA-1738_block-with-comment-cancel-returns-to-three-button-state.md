---
id: ELITEA-1738
title: "Block with Comment — Cancel Returns Dialog to Three-Button State"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1738: Block with Comment — Cancel Returns Dialog to Three-Button State

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that clicking Cancel after expanding the Block with Comment comment input collapses the text area and returns the dialog to the original three-button state without blocking or authorizing the tool.

## Preconditions

- Sensitive tool dialog is displayed (Authorize / Block / Block with Comment visible)
- User has clicked Block with Comment — text area is now expanded

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |
| Comment typed | "Actually, let me reconsider…" (partially typed) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click **Block with Comment** to expand the text area | Text area visible |
| 2 | Type partial comment text | Text appears in the input |
| 3 | Click **Cancel** | Text area collapses; dialog returns to the three-button state (Authorize / Block / Block with Comment) |
| 4 | Verify the tool is still pending | Dialog still visible; tool has not been authorized or blocked |
| 5 | Verify typed text is cleared | Text area is empty if re-opened |
| 6 | Click **Authorize** to complete the flow | Tool executes normally |

## Expected Final State

Cancel dismissed the text area without any action. Subsequent Authorize proceeded normally.

## Pass/Fail Criteria

**Pass:**
- Cancel collapses text area without blocking or authorizing
- Dialog returns to three-button state
- Typed text not submitted or leaked
- Tool still pending after Cancel

**Fail:**
- Cancel closes the entire dialog (tool state unclear)
- Cancel triggers a block without the user confirming
- Dialog disappears or becomes unresponsive
