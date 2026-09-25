---
id: ELITEA-3414
title: "System Token Is Removed on Suspension and Restored on Activation"
priority: low
type: functional
module: tokens
status: draft
execution_type: manual
tags: [feat:tokens, story:5262, system-token, suspension]
requirements: [EliteaAI/elitea_issues#5262]
---
# ELITEA-3414: System Token Lifecycle on Suspend/Activate

**Module:** Tokens · **Priority:** Low · **Type:** Functional

**Objective:** Confirm the expected lifecycle of a user's `elitea-system` token across suspension and reactivation: when a user is suspended, their system token should be removed; when the user is reactivated, the system token should come back.

**Coverage:** AC — system token lifecycle tied to user account state (suspend/activate)

## Preconditions

- A user account that is active and has an `elitea-system` token (confirm via `include_system=True` at the internal/RPC level, since it's not visible in the UI)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm the user currently has an `elitea-system` token. | Confirmed present. |
| 2 | Suspend the user's account. | Account is suspended. |
| 3 | Query the user's tokens with `include_system=True`. | System token is no longer present. |
| 4 | Reactivate the user's account. | Account is active again. |
| 5 | Query the user's tokens with `include_system=True` again. | System token is present again. |

## Expected Final State

The system token's presence tracks the user's active/suspended state: absent while suspended, present while active.

## Pass/Fail Criteria

**Pass:**
- System token is removed immediately on suspension and reappears after reactivation, matching steps 3 and 5

**Fail:**
- System token remains present while the user is suspended
- System token does not come back after reactivation, or a duplicate is created
