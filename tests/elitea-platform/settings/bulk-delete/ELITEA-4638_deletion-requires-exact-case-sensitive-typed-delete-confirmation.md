---
id: ELITEA-4638
title: "Deletion requires exact case-sensitive typed DELETE confirmation"
priority: critical
type: functional
module: settings-delete-project-data
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7189, EliteaAI/elitea_issues#7242]
---

## Preconditions

- User is logged in to `{{base_url}}` as an authorized user (owner/Admin)
- Project has at least one item in at least one entity type

## Test Data

| Input Value | Expected "Delete permanently" State |
|---|---|
| (empty) | Disabled |
| delete | Disabled |
| `DELETE ` (trailing space) | Disabled |
| DELETE! | Disabled |
| DELETE | Enabled |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Check one or more entity-type checkboxes (e.g., Chats) and click "Delete selected data" | Modal opens titled "Delete data from [project name]?" listing selected types and counts |
| 2 | Observe "Delete permanently" default state | Button is disabled |
| 3 | Enter each value from the Test Data table into the confirmation input in turn | Button state matches the table for each value |
| 4 | With "DELETE" entered, click "Cancel" | Modal closes; no data deleted |
| 5 | Reopen Settings → General and check item counts for all types | Counts match pre-test values |
| 6 | Repeat step 1, enter "DELETE," then close the modal via the "X" control instead of Cancel | Modal closes; no data deleted |
| 7 | Recheck item counts | Counts unchanged |

## Expected Final State

No data is deleted at any point in this test; the typed-DELETE gate behaves exactly per the table.

## Pass/Fail Criteria

**Pass:**
- Button enabled only on exact case-sensitive "DELETE"
- Cancel/close never results in deletion

**Fail:**
- Button enabled on a non-exact value
- Any deletion occurs after Cancel or close
