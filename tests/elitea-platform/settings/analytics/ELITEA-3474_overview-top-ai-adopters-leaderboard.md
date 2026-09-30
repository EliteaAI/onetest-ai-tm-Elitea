---
id: ELITEA-3474
title: "Overview Top AI Adopters Leaderboard"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, issue:6145, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437, EliteaAI/elitea_issues#6145]
---
# ELITEA-3474: Overview Top AI Adopters Leaderboard

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Top 5 AI Adopters leaderboard displays correctly and excludes system users.

**Coverage:** Bug #6145 - System entity should not appear in leaderboard.

## Preconditions

- Logged into {{base_url}}
- Project has multiple users with AI activity
- Navigate to Settings → Analytics → Overview

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Locate "Top 5 AI Adopters" section. | Leaderboard section visible with title and info icon. |
| 2 | Verify subtitle shows metric description. | Shows "Leaderboard by AI events (LLM + Tool + Agent / Pipeline)". |
| 3 | Verify up to 5 users are listed. | Maximum 5 users displayed with rank numbers (1-5). |
| 4 | Verify each row shows user avatar and email. | User avatar (colored circle with initial) and email address visible. |
| 5 | Verify each row shows activity breakdown. | Shows "X LLM · Y Tool · Z Agent / Pipeline" format. |
| 6 | Verify each row shows total event count. | Right-aligned total number (sum of LLM+Tool+Agent events). |
| 7 | Verify NO system users appear in list. | No entries with system emails (e.g., system@*, noreply@*). |
| 8 | Verify ranking is by total events descending. | User with highest total is ranked #1. |

## Pass/Fail Criteria

**Pass:** Leaderboard shows top 5 real users ranked by AI events, no system users visible.
**Fail:** System user appears in leaderboard, ranking incorrect, or data missing.
