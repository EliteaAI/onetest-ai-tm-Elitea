---
id: ELITEA-3812
title: "Publishing agent with warning-level skill issues"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with `models.applications.publish.post` permission
- Test agent created with valid base configuration
- Skill with warning-level issue attached (e.g., non-actionable content)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Skill Name | "Descriptive Skill" |
| Skill Content | "This skill is about code review. Code review is important for quality." + additional descriptive text to meet 100 characters requirement |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Attach "Descriptive Skill" to test agent | Skill attached |
| 2 | Click ⋮ menu → **Publish** → complete Preparation | Validation runs |
| 3 | Wait for validation | Result: **WARN** (warnings present, no criticals) |
| 4 | Verify WARNING finding for Skill | Non-actionable content warning shown |
| 5 | Verify **Publish** button state | Button **enabled** |
| 6 | Click **Publish** button | Confirmation dialog appears |
| 7 | Verify warning summary shown | Shows warning-level findings requiring acknowledgment |
| 8 | Confirm publishing | "The agent has been published" toast |
| 9 | Navigate to Agent Hub | Hub loads |
| 10 | Verify agent published | Agent appears in Hub |
| 11 | Add to conversation and test | Agent works, Skill behavior present |

## Expected Final State

Agent with warning-level Skill issues can be published after user acknowledges the warnings. Published agent functions correctly with the Skill.

## Pass/Fail Criteria

**Pass:**
- Warnings require confirmation but don't block publishing
- Agent publishes successfully after warning acknowledgment
- Published agent functions correctly with the Skill

**Fail:**
- Warnings block publishing
- No confirmation required for warnings
- Published agent doesn't function correctly
