---
id: ELITEA-3405
title: "Frequency-tier boundary near the 1-month threshold assigns the correct expiration rule"
priority: medium
type: functional
module: indexing-scheduled-expiration
status: draft
execution_type: manual
tags: [feat:indexer, feat:notifications, eng:backend, nfr:usability, r-2.0.7]
requirements: [EliteaAI/elitea_issues#4997]
---

## Preconditions

- User is logged in to `{{base_url}}` with permission to create scheduled indexing tasks
- Ability to create scheduled tasks with custom intervals near the 1-month threshold

## Test Data

| Interval | Expected Tier |
|----------|----------------|
| Every 4 weeks | High-frequency (90-day expiration) |
| Every 5 weeks / Monthly | Low-frequency (180-day/6x rule) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a task with an interval just under 1 month (e.g., every 4 weeks) | Treated as high-frequency; 90-day expiration applied |
| 2 | Create a task with an interval at/over 1 month (e.g., every 5 weeks or monthly) | Treated as low-frequency; 180-day/6x rule applied |
| 3 | Compare both tasks' stored expiration dates against the tiering rule | Both match documented boundary behavior |

## Expected Final State

Boundary interval tasks are assigned to the correct tier with no ambiguity.

## Pass/Fail Criteria

**Pass:**
- Task with interval just under 1 month receives 90-day expiration
- Task with interval at/over 1 month receives 180-day/6x-rule expiration

**Fail:**
- Either task is misclassified into the wrong frequency tier
- Boundary behavior is inconsistent between equivalent test runs
