---
id: ELITEA-4250
title: Catalog skill usage billed to user's current project
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, catalog, chat, billing, usage, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4250: Catalog skill usage billed to user's current project

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when user runs a Catalog skill published from another project, the usage (tokens/cost) is billed to user's current project, not the skill owner's project.

**Coverage:**
- Chat created in user's current project
- Tokens/cost attributed to user's project
- Skill owner's project NOT charged
- Usage appears in user's project analytics

## Preconditions

- User is logged in to {{base_url}}
- User is in Project A (user's project)
- Catalog has skill published from Project B (different project/owner)
- User has access to analytics/usage page

## Test Data

- User's Project: Project A
- Catalog skill owner's Project: Project B
- Catalog skill: Any published skill from Project B
- Expected: Usage billed to Project A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify user is currently in Project A (check project selector) | User is in Project A |
| 2 | Navigate to Catalog → Skills tab | Catalog displays skills from various projects |
| 3 | Locate a skill published from Project B (different owner) | Skill card shows skill from Project B |
| 4 | Click Run button on the skill from Project B | Chat created with skill participant |
| 5 | Send 2-3 messages to the skill (consume tokens) | Messages sent, skill responds (tokens consumed) |
| 6 | Navigate to Project A → Analytics or Usage page | Analytics page opens |
| 7 | Check usage/token consumption for current period | Usage shows increased token count |
| 8 | Verify Catalog skill is attributed in usage | Skill name appears in usage breakdown/attribution |
| 9 | Check cost attribution | Cost is attributed to Project A (user's project) |
| 10 | (Optional) If possible, check Project B analytics | Project B (skill owner) is NOT charged for user's consumption |
| 11 | Verify chat is listed under Project A's chats | Chat appears in Project A's chat list (not Project B) |

## Expected Final State

Chat created in Project A; tokens/cost billed to Project A; skill owner's Project B not charged; usage in Project A analytics.

## Pass/Fail Criteria

**Pass:** Chat in Project A, usage/cost attributed to Project A, Project B not charged, skill shown in usage breakdown.

**Fail:** Usage billed to Project B (skill owner), or cost attribution incorrect.
