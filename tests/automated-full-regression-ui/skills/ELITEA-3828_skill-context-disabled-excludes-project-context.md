---
id: ELITEA-3828
title: "Verify skill execution excludes project context when toggle is disabled"
priority: critical
type: regression
module: skill-run-settings
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6921]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A skill with "Include project context" toggle set to OFF exists
- Project has project context configured (files, documentation, etc.)
- User has permission to run skills and view execution details

## Test Data

| Field | Value |
|-------|-------|
| Skill | Skill with context toggle OFF |
| Project context | Available in project |
| Test prompt | "Summarize the project" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to skill with context toggle OFF | Skill details page opens |
| 2 | Verify "Run settings" → "Include project context" is OFF | Toggle: OFF |
| 3 | Run skill with prompt that would normally reference project context | Skill execution starts |
| 4 | Wait for execution to complete | Skill run completes |
| 5 | Check API request payload (via network inspector or logs) → Verify system prompt does NOT include project context | System prompt excludes project context |
| 6 | Verify `ignore_project_context: true` in request metadata | Metadata confirms context excluded |
| 7 | Observe skill response → Skill should NOT have access to project-specific information | Response is generic, no project-specific knowledge |
| 8 | Compare with another skill run where context is ON → Verify difference | Context-enabled run includes project info, context-disabled run does not |

## Expected Final State

- Skill execution excludes project context when toggle is OFF
- System prompt does not contain project context
- Skill has no access to project-specific data
- Execution respects ignore_project_context setting

## Pass/Fail Criteria

**Pass:**
- System prompt excludes project context
- Request metadata confirms `ignore_project_context: true`
- Skill response does not contain project-specific information
- Toggle setting correctly controls context inclusion

**Fail:**
- Project context included despite toggle OFF
- System prompt contains project context
- Skill has access to project-specific data
- Toggle setting has no effect
