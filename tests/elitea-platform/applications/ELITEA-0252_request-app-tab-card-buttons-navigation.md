---
id: ELITEA-0252
title: "Request App Tab: Card Buttons Navigation"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0252: Request App Tab: Card Buttons Navigation

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "+ Create App" and "> View Configured" buttons on each card navigate correctly.

**Coverage:**
- DeepWiki "+ Create App" opens creation form pre-set to DeepWiki
- Inventory "+ Create App" opens creation form pre-set to Inventory
- "> View Configured" navigates to Configured tab

## Preconditions

- Logged in as a project member with permission to create apps
- On the Request App tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click '+ Create App' on the DeepWiki card | Creation form opens pre-set to DeepWiki type |
| 2 | Navigate back to the Request App tab | Request App tab is displayed |
| 3 | Click '+ Create App' on the Inventory card | Creation form opens pre-set to Inventory type |
| 4 | Navigate back to the Request App tab | Request App tab is displayed |
| 5 | Click '> View Configured' on either card | Configured tab is shown |

## Expected Final State

Configured tab is shown

## Pass/Fail Criteria

**Pass:**
- All navigations lead to the correct destination
- Correct app type pre-selected in each creation form

**Fail:**
- Wrong type pre-selected, or navigation goes to wrong page
