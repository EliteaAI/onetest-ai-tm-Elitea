---
id: ELITEA-4200
title: "Verify skill execution triggered from chat participant is recorded in Run History (Bug #7215)"
priority: critical
type: regression
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8, bug-area:current-release-scope]
requirements: [EliteaAI/elitea_issues#6921, EliteaAI/elitea_issues#7215]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill exists and is accessible (e.g., "status-report-writer")
- Skill can be added as a chat participant or invoked via chat
- User has permission to run skills and view Run History

## Test Data

| Field | Value |
|-------|-------|
| Skill | status-report-writer or any skill |
| Trigger 1 | Direct run from skill page |
| Trigger 2 | Chat participant invocation |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill details page (e.g., status-report-writer) | Skill page opens |
| 2 | Click "Run" or direct execution button | Skill executes directly |
| 3 | Wait for completion | Run completes |
| 4 | Navigate to skill's Run History tab | Run History displayed |
| 5 | Verify direct run appears in Run History with timestamp, version, duration | Direct run recorded |
| 6 | Note the current number of runs in history | Run count noted (e.g., 1 run) |
| 7 | Navigate to Chat interface | Chat opens |
| 8 | Add skill as a chat participant OR invoke skill in chat (e.g., using ~skill-name) | Skill invoked in chat context |
| 9 | Send message to trigger skill execution | Skill executes within chat |
| 10 | Wait for skill response | Skill responds in chat |
| 11 | Navigate back to skill's Run History tab | Run History displayed |
| 12 | Verify chat-triggered run appears in Run History | **EXPECTED: Run logged | ACTUAL (Bug): Run NOT logged** |
| 13 | Verify run includes timestamp, version, duration, and trigger source (chat) | **FAILS: Chat run missing** |

## Expected Final State

- All skill executions logged in Run History regardless of trigger source
- Direct runs and chat-triggered runs both appear
- Run History shows accurate timestamp, version, duration for all runs
- Trigger source (direct vs. chat) may be indicated

## Pass/Fail Criteria

**Pass:**
- Chat-triggered skill run appears in Run History
- Run History shows all execution types
- Timestamp, version, duration accurate for chat runs

**Fail (Current State - Bug #7215):**
- Chat-triggered skill run does NOT appear in Run History
- Only direct runs are logged
- Run History incomplete (missing chat executions)

## Notes

This test case documents the known bug #7215. Expected to FAIL until bug is fixed.
