---
id: ELITEA-4630
title: "ELITEA-4630: Skill Auto-Invocation from Chat Based on User Intent"
priority: critical
type: regression
module: chat-skills-integration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, feat:skills, auto-invocation, metadata-matching]
requirements: [EliteaAI/elitea_issues#7126]
---
# ELITEA-4630: Skill Auto-Invocation from Chat Based on User Intent

**Module:** Chat Skills Integration · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that the EliteA chat system can automatically invoke skills from the project's available skills based on user intent and skill metadata matching, even when the skill is NOT explicitly added as a chat participant and the user does NOT provide the exact skill name.

**Coverage:**
- Skill auto-invocation without being explicit participant
- Intelligent skill selection based on user intent
- Metadata matching functionality
- Skill executes and returns response
- Works across different skill types

## Preconditions

- User is logged into {{base_url}}
- Project has skills with descriptive metadata (name, description, tags)
- Example skill: "jira-issue-creator" with metadata indicating it creates Jira issues
- Chat session is open without skill explicitly added as participant

## Test Data

| Field | Value |
|-------|-------|
| Available skill | jira-issue-creator (with metadata: "creates jira issues", tags: [jira, issue, ticket]) |
| Test message | "I need to create a new ticket in Jira for bug fix" |
| Expected behavior | System recognizes intent and invokes jira-issue-creator skill |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open chat without explicitly adding jira-issue-creator as participant | Chat opens with empty or other participants |
| 2 | Type natural language message indicating need for Jira ticket: "I need to create a new ticket in Jira for bug fix" | Message appears in input field |
| 3 | Send the message | Message sends successfully |
| 4 | Observe system behavior | System analyzes intent and available skill metadata |
| 5 | Wait for response | System automatically invokes jira-issue-creator skill |
| 6 | Verify skill execution | Skill executes and responds with Jira ticket creation flow or result |
| 7 | Check response indicates skill was invoked | Response shows skill was auto-selected (may show skill name or execution context) |
| 8 | Try another intent-based request for a different skill | System correctly matches intent to appropriate skill |

## Expected Final State

- System intelligently selects and invokes skills based on user intent
- Skills execute without being explicit participants
- User receives appropriate responses from auto-invoked skills
- Metadata matching works across different skill types

## Pass/Fail Criteria

**Pass:**
- System correctly identifies user intent from natural language
- Appropriate skill is auto-selected based on metadata matching
- Skill executes and returns response
- Works without explicit skill participant or exact name mention

**Fail:**
- System doesn't recognize intent
- No skill is invoked automatically
- Wrong skill is selected
- Feature requires explicit skill participant or ~skill mention

## Notes

**Source functional tests:** ELITEA-4407
**Regression rationale:** High-value AI feature that differentiates EliteA; intelligent skill invocation based on semantic understanding.
**Selected checkpoints:** Intent recognition, metadata matching, automatic skill selection and execution.
