---
id: ELITEA-4338
title: "Verify skill executions triggered from chat interface are recorded in Run History"
priority: critical
type: regression
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6927, EliteaAI/elitea_issues#7215]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill (e.g., "status-report-writer") exists and is accessible via direct run and via chat invocation
- Chat interface supports skill invocation

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Chat URL | `{{base_url}}/app/chat` |
| Skill Name | status-report-writer |
| Chat Command | `/run-skill status-report-writer` or similar |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the skill page | Skill page displays |
| 2 | Run the skill directly from the skill page | Skill executes successfully |
| 3 | Navigate to Skills > Run History | The direct run appears in the history table |
| 4 | Note the current number of runs in the history | Count recorded (e.g., 5 runs) |
| 5 | Navigate to the Chat interface | Chat page loads |
| 6 | Invoke the same skill from within the chat (using chat command or skill mention) | Skill executes successfully within chat context |
| 7 | Verify the skill response appears in the chat thread | Skill output is displayed in chat |
| 8 | Navigate back to Skills > [Skill Name] > Run History | Run History page loads |
| 9 | Verify the chat-triggered run appears in the history table | New run entry is present (count increases by 1) |
| 10 | Check that the run entry includes correct timestamp, version, and duration | Metadata is accurate for the chat-triggered run |
| 11 | Click on the chat-triggered run entry | Conversation restores with chat context |

## Expected Final State

All skill executions, regardless of trigger source (direct run or chat invocation), are logged and displayed in Run History with accurate metadata.

## Pass/Fail Criteria

**Pass:**
- Chat-triggered skill runs appear in Run History
- Run count increases after chat invocation
- Metadata (timestamp, version, duration) is accurate
- Run can be restored from history

**Fail:**
- Chat-triggered runs do NOT appear in Run History (BUG #7215)
- Run count does not increase after chat invocation
- Metadata is missing or incorrect
- Run cannot be restored
