---
id: ELITEA-1211
title: "TC-001: Jira Toolkit Form Renders All 8 Fields in the Exact Specified Order"
priority: critical
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1211: TC-001: Jira Toolkit Form Renders All 8 Fields in the Exact Specified Order

**Module:** Jira Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that opening a new Jira toolkit configuration form renders exactly 8 fields in the visible (non-advanced) section, in the exact order: Name → Description → Jira Configuration → PgVector Configuration → Embedding Model → Api Version → Limit → Labels.

Coverage:
- All 8 required fields are present
- Fields appear in the correct top-to-bottom order
- No extra unexpected fields appear in the visible section
- No required field is missing

## Preconditions

- Logged in as User A on {{base_url}}
- Navigate to Toolkits and initiate creating a new Jira toolkit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits → click Create Toolkit → select Jira toolkit type | Jira toolkit configuration form opens |
| 2 | Scan visible form fields top to bottom (before expanding Advanced Settings) — verify field 1 | Field 1 is 'Name' |
| 3 | Continue scanning — verify field 2 | Field 2 is 'Description' |
| 4 | Continue — verify field 3 | Field 3 is 'Jira Configuration' |
| 5 | Continue — verify field 4 | Field 4 is 'PgVector Configuration' |
| 6 | Continue — verify field 5 | Field 5 is 'Embedding Model' |
| 7 | Continue — verify field 6 | Field 6 is 'Api Version' (with a dropdown, e.g., 'Auto') |
| 8 | Continue — verify field 7 | Field 7 is 'Limit' |
| 9 | Continue — verify field 8 | Field 8 is 'Labels' |
| 10 | Verify no additional fields appear below Labels before Advanced Settings | No unexpected fields are present in the visible section |

## Expected Final State

No unexpected fields are present in the visible section

## Pass/Fail Criteria

PASS:
- Exactly 8 fields visible in exact order: Name, Description, Jira Configuration, PgVector Configuration, Embedding Model, Api Version, Limit, Labels
- No extra fields in the visible section; no fields out of order

FAIL:
- Any field is missing or appears in a wrong position
- Additional unexpected fields appear in the visible section
