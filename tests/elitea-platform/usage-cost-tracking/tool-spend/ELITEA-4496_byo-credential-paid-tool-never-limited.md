---
id: ELITEA-4496
title: "Own (BYO) credential usage of a paid tool is never limited or blocked"
priority: critical
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6980]
---
# ELITEA-4496: Own (BYO) credential usage of a paid tool is never limited or blocked

**Module:** Usage Cost Tracking · **Priority:** Critical · **Type:** Functional

**Objective:** Confirm that a toolkit configured with the user's own provider credential (not the shared platform credential) can always be used regardless of platform/project Tool Spend limits.

**Coverage:**
- BYO-credential call succeeds despite shared-credential limit being exhausted
- BYO-credential usage excluded from the Paid Tools $ limit figure

## Preconditions

- Two toolkit configurations exist for the same paid tool: one using the platform-shared credential, one using a credential the user owns/created themselves
- The platform-shared Tool Spend limit for the feature is already exhausted (shared-credential calls are being denied)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Confirm the shared-credential toolkit is currently denying calls (limit exhausted). | Shared-credential call is refused. |
| 2 | Switch the agent/chat to use the toolkit instance backed by the user's own (BYO) credential. | Toolkit switch succeeds. |
| 3 | Trigger the paid tool again using the BYO-credential toolkit. | Call succeeds, is not blocked by the limit exhausted on the shared credential. |
| 4 | Open Settings → Usage → Paid Tools. | BYO-credential call is NOT counted toward the "$X of $Y" limit figure. |

## Expected Final State

BYO-credential paid-tool usage is recorded as unlimited/exempt and never affected by shared-credential limits.

## Pass/Fail Criteria

**Pass:**
- BYO-credential call succeeds despite shared-credential limit being exhausted
- BYO-credential usage is excluded from the Paid Tools $ limit figure

**Fail:**
- BYO-credential call is blocked or counted toward the shared limit
