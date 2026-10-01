---
id: ELITEA-3679
title: "Analytics — Switching Between Private and Team Project Attributes New Activity Correctly"
priority: high
type: functional
module: analytics
status: draft
execution_type: manual
tags: [feat:analytics, usage, private-project, team-project, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6566]
---
# ELITEA-3679: Analytics — Switching Between Private and Team Project Attributes New Activity Correctly

**Module:** Analytics · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching the active project context mid-session (Private → Team, or Team → Private) correctly attributes the next call to whichever project is active at the time — with no lag or stale attribution to the previously active project.

**Coverage:**
- Switching from Private to Team attributes the next call to the Team project
- Switching back to Private attributes the following call back to the Private project
- No stale attribution to whichever project was active before the switch

## Preconditions

- Logged in to {{base_url}} with access to a Private project and a Team project

## Test Data

| Field | Value |
|-------|-------|
| Message in Private context | "First message in private" |
| Message in Team context | "Second message in team" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch to the Private project. Navigate to Analytics > Overview. Note LLM CALLS (baseline P) | Baseline recorded for the Private project |
| 2 | Switch to the Team project. Navigate to Analytics > Overview. Note LLM CALLS (baseline T) | Baseline recorded for the Team project |
| 3 | Switch back to the Private project and send the first test message | LLM responds |
| 4 | Check Private project's Analytics > Overview | LLM CALLS = P + 1 |
| 5 | Without reloading the app, switch to the Team project and send the second test message | LLM responds |
| 6 | Check Team project's Analytics > Overview | LLM CALLS = T + 1 (not stale-attributed to the Private project) |
| 7 | Switch back to the Private project and check its Analytics > Overview | LLM CALLS is still P + 1 — unaffected by the Team project message in step 5 |

## Expected Final State

Each message is attributed to whichever project was actually active in the UI at the moment it was sent.

## Pass/Fail Criteria

**Pass:**
- Both projects show exactly their own call, with no cross-attribution across the context switch

**Fail:**
- Either call is attributed to the project that was active before the switch, instead of the one active when the message was sent
