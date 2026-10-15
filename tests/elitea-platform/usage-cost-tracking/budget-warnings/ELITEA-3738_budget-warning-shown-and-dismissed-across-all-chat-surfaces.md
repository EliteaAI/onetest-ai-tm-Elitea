---
id: ELITEA-3738
title: "Budget Warnings — Banner Shown on All Chat Surfaces and One Dismissal Applies Project-Wide"
priority: high
type: functional
module: usage-cost-tracking
status: draft
execution_type: manual
tags: [r-2.0.7, enhancement:6439, eng:backend, eng:frontend, feat:admin-platform, feat:notifications, feat:settings, nfr:usability]
requirements: ["EliteaAI/elitea_issues#6439"]
---

# ELITEA-3738: Budget Warnings — Banner Shown on All Chat Surfaces and One Dismissal Applies Project-Wide

**Module:** Usage Cost Tracking · **Priority:** High · **Type:** Functional

**Objective:** Verify that the budget banner appears above the message input on every surface that can call a shared model, and that dismissing it on one surface hides it on all surfaces in the same project.

**Coverage:**
- Banner on existing chat, new conversation, agent, pipeline and skill test panel
- Dismissal is per user + project + scope, not per conversation

## Preconditions

- Logged in to `{{base_url}}` as a test user at **80–89%** of the member limit; Cost Budgets mode = **enforce**; dismissal switch **ON**
- The test project has at least one agent, one pipeline with an LLM node and one skill
- No dismissal stored for the current month (clear the `elitea.budgetWarning.dismissed.*` keys)

## Test Data

| Surface | How to open |
|---------|-------------|
| Existing chat | Chat → open an existing conversation |
| New conversation | Chat → + New conversation |
| Agent | Agents → open agent → run/chat panel |
| Pipeline | Pipelines → open pipeline → run/chat panel |
| Skill test panel | Skills → open skill → test panel |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open each surface from the Test Data table | Banner is shown above the message input with the same %, text and severity on every surface |
| 2 | On the agent surface, click X | Banner hides |
| 3 | Revisit and reload every other surface | Banner is hidden on all of them |

## Expected Final State

The banner stays hidden on every surface in the project until the next level is reached.

## Pass/Fail Criteria

**Pass:**
- Banner present on all 5 surfaces before dismissal
- One dismissal hides it on all surfaces in the project

**Fail:**
- Banner missing on any surface
- Dismissal applies only to the conversation or surface where it was clicked
