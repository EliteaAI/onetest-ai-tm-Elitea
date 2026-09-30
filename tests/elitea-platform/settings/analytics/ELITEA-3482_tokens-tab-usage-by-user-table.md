---
id: ELITEA-3482
title: "Tokens Tab Token Usage by User Table"
priority: critical
type: functional
module: analytics
status: ready
execution_type: manual
tags: [feat:analytics, feat:settings, eng:frontend, issue:6437, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6437]
---
# ELITEA-3482: Tokens Tab Token Usage by User Table

**Module:** Analytics · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Token Usage by User table displays complete token breakdown per user.

## Preconditions

- Logged into {{base_url}}
- Project has multiple users with token usage
- Navigate to Settings → Analytics → Tokens

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Scroll to "Token Usage by User" section. | Table visible with per-user token breakdown. |
| 2 | Verify table columns. | Columns: USER, TOTAL TOKENS, INPUT TOKENS, OUTPUT TOKENS, CACHE READ, CACHE WRITE, SHARE. |
| 3 | Verify user emails are displayed. | Each row shows user email address. |
| 4 | Verify token counts use K/M formatting. | Large numbers formatted (e.g., "34.4K", "34.3K"). |
| 5 | Verify SHARE column shows percentage. | Percentage of total tokens used by each user. |
| 6 | Verify sum of TOTAL TOKENS matches header card. | Sum equals the TOTAL TOKENS card value. |

## Pass/Fail Criteria

**Pass:** Table shows all users with complete token breakdown, shares sum to ~100%.
**Fail:** Missing columns, inconsistent formatting, or totals don't match.
