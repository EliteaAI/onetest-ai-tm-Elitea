---
id: ELITEA-3321
title: "Individual save buttons save changes to correct Agent version independently"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions (e.g., "base", "v1.0")

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 | base - Instructions: "Original instructions for base" |
| Version 2 | v1.0 - Instructions: "Original instructions for v1.0" |
| Version 1 Edit | "Updated instructions for base version" |
| Version 2 Edit | "Updated instructions for v1.0 version" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal comparing base and v1.0 | Modal opens with both versions displayed |
| 2 | Edit Instructions text in Version 1 (base) column to "Updated instructions for base version" | Text updates in Version 1 column only |
| 3 | Click Save button for Version 1 column | Save operation executes, success message appears |
| 4 | Verify Version 1 Instructions field shows the saved changes | Version 1 displays "Updated instructions for base version" |
| 5 | Close the Compare Versions modal | Modal closes |
| 6 | Reopen Compare Versions modal for the same Agent | Modal reopens with fresh data |
| 7 | Verify Version 1 (base) shows the saved changes | Version 1 displays "Updated instructions for base version" |
| 8 | Verify Version 2 (v1.0) remains unchanged | Version 2 still shows "Original instructions for v1.0" |
| 9 | Edit Instructions in Version 2 column to "Updated instructions for v1.0 version" | Text updates in Version 2 column only |
| 10 | Click Save button for Version 2 column | Save operation executes, success message appears |
| 11 | Close and reopen modal | Modal reopens |
| 12 | Verify Version 2 now shows updated text | Version 2 displays "Updated instructions for v1.0 version" |
| 13 | Verify Version 1 still shows its previously saved changes (unchanged by Version 2 save) | Version 1 still displays "Updated instructions for base version" |
| 14 | Repeat Steps 2-13 for Welcome Message field | Welcome Message saves independently per version |
| 15 | Repeat Steps 2-13 for Chat Starter text | Chat Starter text saves independently per version |

## Expected Final State

Each version's changes are saved independently without affecting the other version. Version 1 and Version 2 can be edited and saved separately.

## Pass/Fail Criteria

**Pass:**
- Saving Version 1 does not modify Version 2
- Saving Version 2 does not modify Version 1
- Saved changes persist after closing and reopening modal
- Independent save works for Instructions, Welcome Message, and Chat Starters

**Fail:**
- Saving one version affects the other version
- Changes do not persist after modal close/reopen
- Save button saves both versions instead of only the clicked version
