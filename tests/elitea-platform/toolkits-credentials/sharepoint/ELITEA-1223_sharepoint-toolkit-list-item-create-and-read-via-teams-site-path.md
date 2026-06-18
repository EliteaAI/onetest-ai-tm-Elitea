---
id: ELITEA-1223
title: "SharePoint Toolkit — List Item Create and Read via /teams/ Site Path"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1223: SharePoint Toolkit — List Item Create and Read via /teams/ Site Path

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that Create list item, Read list, Get list columns, and Add attachment to list item tools operate correctly against a /teams/ site. Covers: Get list columns returns schema; Create list item adds a record; Read list returns the created item; Add attachment succeeds.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- SharePoint toolkit with Site Path teams/TestTeam, tools Get list columns, Create list item, Read list, Add attachment to list item all enabled
- A test SharePoint list (QA Test List) exists in the /teams/ site with at least one required text field
- A test file available in ELITEA Artifacts for attachment

## Test Data

Site Path: teams/TestTeam
List name: QA Test List
New item: {"Title": "QA Automated Item"}
Attachment file: test.txt from Artifacts

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Test Settings, select Get list columns. Provide list name QA Test List. Click Run Tool. | Column metadata returned: field names, display names, types, required flags. No HTTP errors. |
| 2 | Select Create list item. Provide list name QA Test List and {"Title": "QA Automated Item"}. Click Run Tool. | Success response. New item ID returned. No HTTP 4xx/5xx. |
| 3 | Select Read list. Provide list name QA Test List. Click Run Tool. | Item with Title = 'QA Automated Item' appears in the returned list items. |
| 4 | Select Add attachment to list item. Provide list name QA Test List, the item ID from step 2, and test.txt. Click Run Tool. | Success response. No HTTP errors. |

## Expected Final State

Success response. No HTTP errors.

## Pass/Fail Criteria

Pass:
- All four list operations succeed against the /teams/ site
- Created item is visible in Read list output
- Attachment is added without error

Fail:
- Any operation returns HTTP error or 'list not found' referencing the wrong site
- Created item does not appear in Read list
- Add attachment fails with permission or path error
