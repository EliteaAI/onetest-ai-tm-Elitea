---
id: ELITEA-1170
title: "TC-005: Confluence Toolkit Form Renders All 9 Fields in the Exact Specified Order"
priority: critical
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1170: TC-005: Confluence Toolkit Form Renders All 9 Fields in the Exact Specified Order

**Module:** Confluence Toolkit Configuration · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Confluence toolkit creation form renders all 9 specified fields in the exact required order, and that all labels and input types match the specification.

Required field order:
1. Toolkit Name
2. Base URL
3. Username/Email
4. API Token
5. Space Keys
6. Connection Type
7. Cloud (if applicable)
8. Pages Limit
9. Labels

Coverage:
- All 9 fields present and nothing extra
- Fields appear in the exact specified order (top to bottom)
- Each field has correct label and input type

## Preconditions

- Logged in as User A
- Confluence toolkit creation form open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Toolkits section and open the Confluence toolkit creation form | Confluence toolkit creation form opens |
| 2 | Identify the first field at the top of the form (before Advanced Settings) | Field 1: Toolkit Name (text input) |
| 3 | Identify fields 2 through 9 in sequence | In order: Base URL (text), Username/Email (text), API Token (password), Space Keys (text/multi), Connection Type (dropdown), Cloud (toggle/checkbox — if applicable), Pages Limit (number), Labels (tag/multi-select) |
| 4 | Check the Advanced Settings section is present but collapsed (not counted as a main field) | Advanced Settings accordion visible below the main 9 fields |
| 5 | Verify no extra fields appear outside of Advanced Settings | Exactly 9 visible fields listed; no extra unlabelled or unexpected inputs present |

## Expected Final State

Exactly 9 visible fields listed; no extra unlabelled or unexpected inputs present

## Pass/Fail Criteria

PASS:
- All 9 specified fields appear, in exact order, with correct labels and input types

FAIL:
- Any field is missing, appears in wrong position, or has wrong label
- Extra fields appear that are not in the specification
- Any field has an incorrect input type (e.g., text instead of toggle)
