---
id: ELITEA-3676
title: "Budget — Project Over Limit Blocks Further Calls With a Clear Message"
priority: critical
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, budget, enforcement, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566, EliteaAI/elitea_issues#6573]
---
# ELITEA-3676: Budget — Project Over Limit Blocks Further Calls With a Clear Message

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that once a project's budget limit is reached, further chat/agent calls in that project are blocked, and the user sees a clear, readable message explaining why.

**Coverage:**
- Over-limit project blocks new calls
- Refusal message is clear and persists after a page refresh

## Preconditions

- **Requires a project already over its configured budget limit** (e.g. a dedicated over-budget test project) — if none is available, this case cannot be executed yet; flag with the environment/admin owner to get access to one

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Hello" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Confirm the project's Usage/Budget page shows the limit as reached (percent-used at/above 100%) | Over-limit state confirmed |
| 2 | Send a chat message in the project | Request is refused |
| 3 | Read the message shown in the chat response | A clear, human-readable message explains the budget has been reached — visible directly in the response, no need to dig through debug/technical details |
| 4 | Refresh the page | The refusal message is still visible after refresh (doesn't disappear) |

## Expected Final State

Over-limit projects are blocked from new calls, and the user is shown a clear, persistent explanation.

## Pass/Fail Criteria

**Pass:**
- Call is blocked
- Message is clear and understandable without extra steps, and survives a page refresh

**Fail:**
- Call is not blocked despite being over budget
- Message is unclear/generic, hidden behind extra steps, or disappears after refresh
