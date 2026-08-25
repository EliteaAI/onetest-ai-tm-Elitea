---
id: ELITEA-2769
title: "Suggested Name field respects existing character limit truncation behavior"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5893]
---

## Preconditions

- User is logged in with Editor or Admin role
- An existing Agent's configuration page is open
- The standard Agent Name field's character limit is known (matches the limit enforced on the standard agent creation/edit form)

## Test Data

| Field | Value |
|-------|-------|
| Prompt | "Rename the agent to something very descriptive" |
| Paste string | 40+ character string exceeding the Name field's limit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing Agent and initiate Edit with AI | Modal opens |
| 2 | Enter prompt "Rename the agent to something very descriptive" | Prompt accepted |
| 3 | Generate the draft and navigate to the General step | Suggested Name field shown, editable |
| 4 | Attempt to manually type characters beyond the field's character limit | Additional characters beyond the limit cannot be entered |
| 5 | Clear the field and paste a 40+ character string into the Suggested Name field | The pasted text is truncated to the field's character limit |
| 6 | Complete the wizard and apply changes | Modal closes without error |
| 7 | Verify the saved Agent Name | Name matches the truncated value, not the full pasted string |

## Expected Final State

The Suggested Name field enforces the same character limit and truncation-on-paste behavior as the standard Agent Name field, and the persisted Agent Name reflects that limit.

## Pass/Fail Criteria

**Pass:**
- Typing beyond the limit is blocked and pasted overflow text is truncated to the field's character limit, both before and after applying

**Fail:**
- Typing or pasting allows the Suggested Name to exceed the standard character limit, or the saved Agent Name exceeds the limit
