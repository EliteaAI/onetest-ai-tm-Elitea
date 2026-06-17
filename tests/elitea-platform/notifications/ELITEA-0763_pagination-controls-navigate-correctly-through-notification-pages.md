---
id: ELITEA-0763
title: "Pagination Controls Navigate Correctly Through Notification Pages"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, story:4431, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4431]
---
# ELITEA-0763: Pagination Controls Navigate Correctly Through Notification Pages

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Notification Center table pagination works correctly: next/previous navigation, rows-per-page selector, and current range indicator — consistent with the Settings → Users table.

**Coverage:**
- Pagination controls present at the bottom of the table
- Rows-per-page selector with standard options (10, 20, 50)
- Current range indicator shows correct values
- Next/Previous navigation works
- Next disabled on last page; Previous disabled on first page

## Preconditions

- Logged in to {{base_url}}
- More notifications than one page size (to trigger pagination)

## Test Data

- URL: {{base_url}}
- Rows-per-page values to test: 10, 20, 50

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/notification-center | Notification Center table is displayed with pagination controls |
| 2 | Verify a rows-per-page selector is present with options including 10, 20, and 50 | Rows-per-page selector with multiple options is visible |
| 3 | Change rows-per-page to 10 | Exactly 10 rows (or fewer on last page) are displayed |
| 4 | Verify the range indicator shows correctly (e.g., '1–10 of 45') | Range indicator is accurate |
| 5 | Click Next page | Table shows the next set of notifications and range indicator updates |
| 6 | Click Previous page | Previous set of notifications is shown |
| 7 | Navigate to the last page | Next button is disabled or absent |
| 8 | Navigate back to page 1 | Previous button is disabled or absent |

## Expected Final State

Previous button is disabled or absent

## Pass/Fail Criteria

**Pass:**
- All pagination controls function correctly
- Range indicator is accurate at all times
- Edge page buttons are correctly disabled

**Fail:**
- Pagination controls are absent
- Next/Previous navigation shows wrong page
- Range indicator is inaccurate
- Edge page buttons are not disabled
