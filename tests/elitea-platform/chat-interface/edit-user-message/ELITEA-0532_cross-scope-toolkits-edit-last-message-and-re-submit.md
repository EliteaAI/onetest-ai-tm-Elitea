---
id: ELITEA-0532
title: "Cross-scope — Toolkits: edit last message and re-submit"
priority: critical
type: functional
module: edit-user-message
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0532: Cross-scope — Toolkits: edit last message and re-submit

**Module:** Edit User Message · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the edit-and-resubmit feature works correctly in Toolkit chat context.

**Coverage:**
- Edit icon present on last user message in Toolkit chat
- Save and apply re-executes toolkit with updated input
- Previous response replaced

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A Toolkit is configured and accessible
- At least one user-assistant exchange exists in the Toolkit chat

## Test Data

- Toolkit: any available Toolkit
- Original message: "Search for recent news"
- Edited message: "Search for recent sports news"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to a Toolkit. Send "Search for recent news" and wait for the response. | Toolkit processes and returns results. |
| 2 | Verify Edit icon on the last user message. Click it. | Edit mode opens inline. |
| 3 | Change text to "Search for recent sports news" and click "Save and apply". | Toolkit re-executes with updated input. Loading state shown. |
| 4 | Verify the new response. | Response reflects the updated query (sports news). Previous response is replaced. |

## Expected Final State

Response reflects the updated query (sports news). Previous response is replaced.

## Pass/Fail Criteria

**Pass:**
- Edit feature works in Toolkit context
- Toolkit re-executes with updated input
- Previous response replaced

**Fail:**
- Edit icon missing in Toolkit chat
- Toolkit does not re-execute
- Feature behaves differently than other contexts
