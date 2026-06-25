---
id: ELITEA-1735
title: "Block with Comment — Button Visible and Expands Comment Input Field"
priority: critical
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1735: Block with Comment — Button Visible and Expands Comment Input Field

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the HITL authorization dialog shows three actions — Authorize, Block, and Block with Comment — and that clicking "Block with Comment" expands a text input for the user to enter a reason.

## Preconditions

- At least one sensitive tool is configured (e.g., `aa.create_new_bucket`)
- Agent chat is open with authorization dialog currently displayed

## Test Data

| Field | Value |
|-------|-------|
| Tool | Any tool marked as sensitive in guardrails configuration |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger the agent to call the sensitive tool | Authorization dialog appears with "Sensitive Action Authorization Required" heading |
| 2 | Inspect the action buttons in the dialog | Three buttons visible: **Authorize** (green), **Block** (red), **Block with Comment** (grey/outlined) |
| 3 | Click the **Block with Comment** button | Dialog expands to reveal a multi-line text input field with placeholder text (e.g., "Tell the agent why this call is blocked and what to do instead. Press ⌘/Ctrl+Enter to send.") |
| 4 | Verify the original Authorize and Block buttons remain visible | Authorize and Block buttons still shown; Block with Comment button remains visible or transforms to confirm action |
| 5 | Verify a Cancel option is available | A Cancel link/button is shown to dismiss the comment input without submitting |

## Expected Final State

Dialog shows Authorize, Block, and Block with Comment actions. Clicking Block with Comment reveals the comment text area without closing the dialog.

## Pass/Fail Criteria

**Pass:**
- All three action buttons present in initial dialog
- Block with Comment expands a text input inline
- Placeholder text instructs the user on how to submit
- Cancel option available to collapse the input

**Fail:**
- Block with Comment button absent
- Clicking Block with Comment closes dialog without showing text input
- No Cancel / dismiss option available
- Only one or two action buttons shown
