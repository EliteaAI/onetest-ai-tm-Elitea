---
id: ELITEA-3819
title: "Publishing flow without skills - unaffected"
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
- Test agent created with valid configuration (name, description, instructions, tags, icon)
- Agent has NO Skills attached (SKILLS section empty: 0/5)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "No Skills Agent" |
| Skills Attached | 0 (none) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "No Skills Agent" | Agent configuration loads |
| 2 | Verify SKILLS section | Shows "0/5" - no Skills attached |
| 3 | Click ⋮ menu → **Publish** | Publish wizard opens |
| 4 | Verify Preparation step | Same fields as always: version, category, terms |
| 5 | Verify Publishing Terms content | Terms do NOT specifically highlight "0 Skills" or add Skill-specific warnings |
| 6 | Complete Preparation step | Continue to Validation |
| 7 | Wait for validation to complete | Result: **PASS** (assuming agent valid) |
| 8 | Review validation results categories | Standard categories: Name, Description, Instructions, Icon, Tags, etc. |
| 9 | Verify NO "Skills" section in validation | No Skills category appears (nothing to validate) |
| 10 | Click **Publish** | "The agent has been published" toast |
| 11 | Navigate to Agent Hub | Hub loads |
| 12 | Verify published agent appears | Agent card visible in Hub |
| 13 | Add to conversation and test | Agent works normally |

## Expected Final State

Publishing workflow for agents without Skills remains unchanged. No Skills-related sections or findings appear in validation. Agent publishes and works normally.

## Pass/Fail Criteria

**Pass:**
- Publishing wizard unchanged for agents without Skills
- Validation results do NOT show Skills section/category
- No Skills-related findings appear (nothing to validate)
- Agent publishes and works normally

**Fail:**
- Publishing flow different for agents without Skills
- Skills section appears in validation for agent with no Skills
- Agent fails to publish or work correctly
