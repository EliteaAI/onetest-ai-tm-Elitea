---
id: ELITEA-4846
title: "Keep all chat starters when copying an agent that is above the limit"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7322]
---

## Preconditions

- User is logged in to `{{base_url}}` as a platform admin who is a member of a team project
- The platform limit M is set to 3 (restore the original value at the end)
- A source agent has 8 chat starters
- A public agent with more than 3 chat starters exists in the Public catalog

## Test Data

| Copy operation | Source | Expected starters |
|----------------|--------|-------------------|
| Save As Version (editor) | Source agent, 8 | 8 in source order |
| Fork to the team project | Source agent, 8 | 8 in source order |
| Fork from Public into {{project_id}} | Public agent, K > 3 | K in source order, plus tags and welcome message (#7059) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | On the source agent use Save As Version | The new version is created with no limit error |
| 2 | Open the new version's editor and hover + Starter | "8/3" over limit, all 8 in source order, over-limit tooltip |
| 3 | Fork the source agent to the team project | The fork completes with no limit error |
| 4 | Open the forked agent in the team project | "8/3" over limit, all 8 in source order |
| 5 | Fork the public agent from the Public catalog into your project | The fork completes with no limit error |
| 6 | Open the Public fork | "K/3" over limit, K starters in order; tags and welcome message carried over |
| 7 | Open a new chat with the Public fork as participant | All K starters are reachable |
| 8 | Delete the copies and forks and restore the original limit; check the source | The source still has 8 |

## Expected Final State

Every copy has all of its source's starters. No copy operation is blocked by M.

## Pass/Fail Criteria

**Pass:**
- All three copy operations keep every starter in order, with no limit error

**Fail:**
- A copy loses or reorders starters, or a copy operation fails with a limit error
- The Public fork loses its tags or welcome message
