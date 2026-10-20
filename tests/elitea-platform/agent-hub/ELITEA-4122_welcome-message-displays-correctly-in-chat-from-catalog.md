---
id: ELITEA-4122
title: "Verify welcome message displays correctly in chat after starting session from catalog"
priority: high
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A published agent exists with a welcome message long enough to be clamped in the catalog card

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents-studio` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In Agents Studio, locate the test agent's card and click "Show more" to view/record the full welcome message | Full text is displayed and recorded |
| 2 | From the same card, start a chat session with the agent | Chat interface opens |
| 3 | Observe the welcome message as displayed in the chat interface | Welcome message is visible in the chat UI |
| 4 | Compare the chat-displayed welcome message against the text recorded in step 1 and against the editor's saved content | Text matches exactly in both comparisons |

## Expected Final State

The chat interface displays the complete, untruncated welcome message, consistent with the catalog's expanded view and the editor's saved content.

## Pass/Fail Criteria

**Pass:**
- Welcome message in chat is complete, untruncated, and matches both the catalog's expanded view and the editor's saved text exactly

**Fail:**
- Welcome message in chat is truncated, missing, or differs from the catalog/editor text
