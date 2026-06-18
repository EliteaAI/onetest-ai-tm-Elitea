---
id: ELITEA-0533
title: "Cross-scope — Pipelines: edit last message and re-submit"
priority: critical
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0533: Cross-scope — Pipelines: edit last message and re-submit

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the edit-and-resubmit feature works correctly in Pipeline chat context.

**Coverage:**
- Edit icon present on last user message in Pipeline chat
- Save and apply re-runs pipeline with updated input
- Previous response replaced

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A Pipeline is configured and accessible
- At least one user-assistant exchange exists in the Pipeline chat

## Test Data

- Pipeline: any available Pipeline
- Original message: "Summarize AI trends"
- Edited message: "Summarize cloud computing trends"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Pipeline. Send "Summarize AI trends" and wait for the response. | Pipeline processes and returns a response about AI trends. |
| 2 | Verify Edit icon on the last user message. Click it. | Edit mode opens inline. |
| 3 | Change text to "Summarize cloud computing trends" and click "Save and apply". | Pipeline re-runs with updated input. Loading state shown. |
| 4 | Verify the new response. | Response is about cloud computing trends. Previous AI trends response is replaced. |

## Expected Final State

Response is about cloud computing trends. Previous AI trends response is replaced.

## Pass/Fail Criteria

**Pass:**
- Edit feature works in Pipeline context
- Pipeline re-runs with updated input
- Previous response replaced

**Fail:**
- Edit icon missing in Pipeline chat
- Pipeline does not re-run
- Both old and new responses visible
