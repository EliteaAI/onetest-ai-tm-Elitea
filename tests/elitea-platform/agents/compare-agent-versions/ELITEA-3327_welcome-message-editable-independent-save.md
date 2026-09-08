---
id: ELITEA-3327
title: "Welcome Message field is editable and saves independently for each Agent version"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions containing different Welcome Messages

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version 1 Welcome Message | "Welcome to Version 1! How can I assist you today?" |
| Version 2 Welcome Message | "Hello! This is Version 2. Let me know how I can help." |
| Version 1 Edit | "Updated welcome message for Version 1 only" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent | Modal opens successfully |
| 2 | Navigate to User Interaction section | Section loads |
| 3 | Verify Welcome Message fields are displayed for both versions | Welcome Message text areas visible in both columns |
| 4 | Verify Version 1 shows: "Welcome to Version 1! How can I assist you today?" | Correct content displayed |
| 5 | Verify Version 2 shows: "Hello! This is Version 2. Let me know how I can help." | Correct content displayed |
| 6 | Verify differences are highlighted between the two Welcome Messages | Diff highlighting visible on changed text |
| 7 | Click on Version 1 Welcome Message field | Field is editable, cursor appears |
| 8 | Edit Version 1 Welcome Message to "Updated welcome message for Version 1 only" | Text updates in Version 1 field only |
| 9 | Verify Version 2 Welcome Message remains unchanged | Version 2 still shows original text |
| 10 | Click Save button for Version 1 | Save operation executes, success message appears |
| 11 | Verify Version 1 Welcome Message field shows the saved changes | Field displays "Updated welcome message for Version 1 only" |
| 12 | Close the Compare Versions modal | Modal closes |
| 13 | Reopen Compare Versions modal | Modal opens with fresh data |
| 14 | Verify Version 1 Welcome Message shows the saved changes | Field displays "Updated welcome message for Version 1 only" |
| 15 | Verify Version 2 Welcome Message is unchanged | Version 2 still shows "Hello! This is Version 2. Let me know how I can help." |

## Expected Final State

Welcome Message field is editable for both versions, saves independently per version, and changes persist after modal close/reopen.

## Pass/Fail Criteria

**Pass:**
- Welcome Message fields are displayed and editable for both versions
- Saving Version 1 does not affect Version 2
- Changes persist after modal close and reopen
- Diff highlighting shows differences before editing

**Fail:**
- Welcome Message fields are missing or read-only
- Saving one version affects the other
- Changes do not persist
- No diff highlighting
