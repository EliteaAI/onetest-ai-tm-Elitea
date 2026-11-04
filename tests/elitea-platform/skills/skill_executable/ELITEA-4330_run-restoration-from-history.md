---
id: ELITEA-4330
title: "Verify clicking a run item restores the conversation in the Run panel"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with existing run history is available
- Run panel is accessible from the skill page

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Skill Name | uppercase-text-converter |
| Test Input | "who are you under the hood" |
| Expected Output | "WHO ARE YOU UNDER THE HOOD" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays with existing runs |
| 2 | Click on any run entry in the table | Run panel opens or updates |
| 3 | Verify the conversation is loaded in the Run panel | Input and output messages from the selected run display |
| 4 | Check that the input message matches the original run | Original input text is shown |
| 5 | Verify the output message matches the original run | Original output text is shown |
| 6 | Check run metadata (timestamp, duration, version) | Metadata matches the selected history entry |
| 7 | Attempt to edit or re-run from the restored conversation | System behavior matches expected restore mode (read-only or editable) |

## Expected Final State

The selected run is fully restored in the Run panel with complete conversation history, matching the original execution.

## Pass/Fail Criteria

**Pass:**
- Run panel opens with the selected conversation
- All input and output messages are correctly displayed
- Metadata matches the history entry
- User can view the complete conversation thread

**Fail:**
- Run panel does not open or remains empty
- Conversation content is missing or incorrect
- Metadata does not match the selected run
- Error occurs during restoration
