---
id: ELITEA-4497
title: "Project-level paid-tool monthly limit is enforced across all project members"
priority: critical
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4497: Project-level paid-tool monthly limit is enforced across all project members

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that a project-level monthly USD limit configured for a paid tool (e.g. Web Search) is enforced once total project usage reaches it, regardless of which member generates the usage.

**Coverage:**
- All members denied once the project limit is reached
- BYO credential calls remain unaffected by the project limit

## Preconditions

- A low, known project-level monthly USD limit is already configured for the paid tool on the test project
- Test project has at least two members

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/usage` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As a project member, trigger paid-tool calls until the Settings → Usage → Paid Tools progress bar for the project reaches the configured project limit. | Progress bar reaches/exceeds 100% of the project limit. |
| 2 | Trigger one more paid-tool call from the same member. | Call is denied (tool unavailable); conversation continues. |
| 3 | Trigger a paid-tool call from a different member of the same project. | Call is also denied, since the project-level limit applies across all members. |
| 4 | Trigger a call using a BYO credential from either member. | Call succeeds and is not counted toward the project limit. |

## Expected Final State

Once the project-level limit is reached, all members are denied further shared-credential paid-tool calls; BYO calls remain unaffected.

## Pass/Fail Criteria

**Pass:**
- All members are denied once the project limit is reached
- BYO credential calls remain unaffected

**Fail:**
- Any member can exceed the project-level limit via the shared credential
