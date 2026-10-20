---
id: ELITEA-4119
title: "Verify full welcome message/description text is accessible via show-more and matches editor content"
priority: critical
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#6861]
---

## Preconditions

- User is logged in to `{{base_url}}` with permissions to create, edit, and publish agents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents-studio` |
| Welcome message | Long text exceeding the 8-line card clamp (e.g. multiple sentences, 500+ characters) |
| Description | Long text exceeding the 2-line card clamp |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the agent editor and create a new agent | Editor opens with empty fields |
| 2 | Enter the long welcome message from Test Data; note the exact text | Text is accepted, "characters left" counter updates |
| 3 | Enter the long description from Test Data; note the exact text | Text is accepted |
| 4 | Save and publish the agent | Agent is published successfully |
| 5 | Open Agents Studio and locate the published agent's card | Card is visible in the catalog |
| 6 | Observe the welcome message area on the card | Text is visually clamped (cut off) and a "Show more" control is visible |
| 7 | Click "Show more" on the welcome message | Full, untruncated welcome message is displayed |
| 8 | Compare the displayed text to the text entered in step 2 | Text matches exactly, character-for-character, with no mid-word cut-off |
| 9 | Click "Show less" / collapse the welcome message | Card returns to its clamped state with no errors |
| 10 | Repeat steps 6–9 for the description field | Description clamps/expands/collapses correctly and matches step 3 text exactly |

## Expected Final State

The agent card returns to its original clamped state for both fields after collapsing; no errors or layout issues occur.

## Pass/Fail Criteria

**Pass:**
- "Show more" is visible for both truncated fields
- Expanded text exactly matches the text entered in the editor for both fields
- Collapsing returns to the original clamped view without errors

**Fail:**
- "Show more" is missing when text is visually clamped
- Expanded text differs from the editor-saved text (missing, duplicated, or corrupted characters)
- Errors or broken layout occur on expand/collapse
