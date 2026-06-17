---
id: ELITEA-0758
title: "Backend-Powered Search Returns Results Across All Pages"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0758: Backend-Powered Search Returns Results Across All Pages

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify search is powered by the backend and returns results from beyond the current visible page — confirming it is not a client-side-only filter.

**Coverage:**
- Search returns a notification that exists on page 2 or later while on page 1
- Pagination updates to reflect the filtered result set

## Preconditions

- Logged in to {{base_url}}
- Enough notifications to span at least 2 pages (e.g., more than 20 if page size is 20)
- A known notification on page 2 or beyond with a unique identifiable term

## Test Data

- URL: {{base_url}}
- Identify a notification only visible on page 2+ (e.g., an older index name)
- Search keyword: the unique term from that page-2 notification

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/notification-center and confirm you are on page 1 | Page 1 of notifications is displayed |
| 2 | Navigate to page 2 and identify a notification with a term NOT visible on page 1 — note the term | A unique page-2 notification term is identified |
| 3 | Return to page 1 and type the noted search term into the Search input | Search is triggered |
| 4 | Verify the page-2 notification appears in the filtered results | The page-2 notification is returned in search results from page 1 |
| 5 | Verify the pagination or result count updates to reflect only the filtered set | Pagination adjusts to the filtered count |

## Expected Final State

Pagination adjusts to the filtered count

## Pass/Fail Criteria

**Pass:**
- Page-2 notification appears in search results from page 1
- Pagination adjusts to reflect the filtered result count

**Fail:**
- Only page-1 notifications are returned in search results
- Page-2 notification is missed by the search
