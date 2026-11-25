---
id: ELITEA-4526
title: "Verify the Test page's Model selector does not affect Tavily tool validation, and Model Settings apply/cancel correctly"
priority: critical
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit, open on its "Test Toolkit" page

## Test Data

| Field | Value |
|-------|-------|
| Model Settings | Reasoning slider, Max Completion Tokens, Capabilities badges |
| Out-of-range test | Max Depth above its ceiling (reused from an earlier case) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "Model Settings" (gear icon) | Dialog shows Reasoning slider, Max Completion Tokens, Capabilities badges |
| 2 | Change the Reasoning slider and click "Cancel", then reopen Model Settings | Change was discarded; still at the original value |
| 3 | Change the Reasoning slider and click "Apply" (if enabled), then reopen Model Settings | Change persisted for this test session |
| 4 | Switch the Model dropdown to a different available model, re-run the out-of-range Max Depth test | Same validation message/behavior occurs regardless of which model is selected |

## Expected Final State

The Model selector and its settings are confirmed independent of Tavily's own field validation.

## Pass/Fail Criteria

**Pass:**
- Cancel discards changes
- Apply persists them
- Model choice never affects Tavily-specific validation behavior

**Fail:**
- Cancel fails to discard a change
- Apply fails to persist it
- Switching models changes validation behavior
