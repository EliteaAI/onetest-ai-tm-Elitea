---
id: ELITEA-4498
title: "Member-level paid-tool monthly limit is enforced individually without blocking other members"
priority: critical
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4498: Member-level paid-tool monthly limit is enforced individually without blocking other members

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that a per-member monthly USD limit configured for a paid tool is enforced individually for that member, without blocking other members of the same project.

**Coverage:**
- Restricted member is denied at their own limit
- Other members remain unaffected while the project-level total stays under its own limit

## Preconditions

- A low, known member-level monthly USD limit is already configured for one specific member of a team project
- The overall project-level limit is not yet reached

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the member with the configured member-level limit, trigger paid-tool calls until that member's usage reaches their configured limit. | Member's usage reaches/exceeds their limit. |
| 2 | Trigger one more paid-tool call as that member. | Call is denied, even though the project-level limit has not been reached. |
| 3 | As a different member of the same project (without a member-level limit, or with a higher one), trigger a paid-tool call. | Call succeeds. |
| 4 | Open Settings → Usage. | Restricted member's usage shows at/over their member limit; project-level total remains below the project limit. |

## Expected Final State

The member-level limit restricts only that specific member; other members remain unaffected while the project-level total stays under its own limit.

## Pass/Fail Criteria

**Pass:**
- Restricted member is denied at their own limit
- Other members remain unaffected

**Fail:**
- Member-level limit incorrectly blocks other members, or fails to block the restricted member
