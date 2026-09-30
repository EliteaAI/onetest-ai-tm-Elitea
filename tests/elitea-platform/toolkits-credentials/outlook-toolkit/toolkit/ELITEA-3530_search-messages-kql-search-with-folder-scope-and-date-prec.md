---
id: ELITEA-3530
title: "search_messages — KQL Search With Folder Scope and Date Precision"
priority: critical
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3530: search_messages — KQL Search With Folder Scope and Date Precision

**Module:** Outlook Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify `search_messages` correctly applies a KQL query, restricts results to the given folder scope, and that date filters only have day-level precision (the documented KQL caveat).

## Preconditions

- Test mailbox has messages with distinct subjects across multiple folders and known received dates
- Toolkit with `search_messages` enabled

## Test Data

- KQL query: `subject:"Outlook Toolkit Test"`
- Folder scope: `Inbox`
- Date filter: a specific date matching one of the test messages, e.g. `2026-09-25`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `search_messages` with the KQL query, no folder scope | Matching messages returned across all folders |
| 2 | Invoke `search_messages` with the same query and `folder=Inbox` | Only matches within Inbox are returned |
| 3 | Invoke `search_messages` with a date filter for a specific day | All messages from that calendar day are returned regardless of time-of-day, confirming day-level (not time-level) precision |

## Expected Final State

Search results correctly reflect the KQL query, folder scope, and day-precision date filtering.

## Pass/Fail Criteria

**Pass:**
- KQL matching works as expected
- Folder scoping correctly restricts results
- Date filter matches the whole day, not a specific time

**Fail:**
- Folder scope is ignored (results leak from other folders)
- Date filter behaves with unexpected time-level precision or misses same-day messages
