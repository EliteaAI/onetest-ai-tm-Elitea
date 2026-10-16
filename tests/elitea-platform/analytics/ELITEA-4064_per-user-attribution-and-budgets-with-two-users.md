---
id: ELITEA-4064
title: "Usage, cost and budget are attributed to the user who ran the agent"
priority: high
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, budget, users, r-2.0.7]
requirements: ["EliteaAI/elitea_issues#6566"]
---

# ELITEA-4064: Usage, cost and budget are attributed to the user who ran the agent

**Module:** analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that runs by two different users (including a viewer who can only run agents) are attributed to the right user in run detail, users list, agent detail and budgets.

---

## Preconditions

- Two users in the project: an admin and a viewer.
- An agent both can run; one shared model and one project-own model.

---

## Test Data

| Field | Value |
|-------|-------|
| Runs | Each user runs a plain and a tool prompt on both models |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Record both users' budget spend and requests. | Baseline. |
| 2 | Run the prompts as each user. | All succeed (the viewer can run the agent). |
| 3 | Check run detail for each run. | `user_id` is the user who ran it. |
| 4 | Check the users list and the agent detail users table. | Each user's LLM and tool events equal their own runs. |
| 5 | Check both users' budget change. | Each increases by the cost of their own shared-model calls only. |
| 6 | Check Activity. | Both users counted as active. |

---

## Expected Final State

Every run, cost and budget change belongs to the user who made it.

---

## Pass/Fail Criteria

**Pass:**
- All attribution and budget deltas match per user.

**Fail:**
- Runs attributed to the wrong user, or budgets changed for the wrong user or by own-model calls.
