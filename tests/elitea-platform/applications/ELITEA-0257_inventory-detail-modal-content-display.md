---
id: ELITEA-0257
title: "Inventory Detail Modal: Content Display"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0257: Inventory Detail Modal: Content Display

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Inventory detail modal opens via the chip click and displays all required content correctly.

**Coverage:**
- Modal opens on inventory chip click with background overlay
- Title, icon, primary description, use-case line, "What it includes" section, and three capability chips

## Preconditions

- Logged in as a project member
- On the Request App tab

## Test Data

Expected capability chips: 'Component inventory', 'Dependency discovery', 'Ownership context'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the 'inventory' chip on the Inventory card | Modal opens; background overlay is applied |
| 2 | Observe the modal title | 'Inventory' is displayed |
| 3 | Observe the modal icon | Placeholder/puzzle icon is shown |
| 4 | Observe the primary description | 'Explore services, ownership, dependencies, and technical inventory across project repositories.' |
| 5 | Observe the use-case line | 'Teams coordinating modernization, impact analysis, service discovery, or engineering governance.' |
| 6 | Observe the 'What it includes' section header | Section header is visible |
| 7 | Observe the capability chips | 'Component inventory', 'Dependency discovery', and 'Ownership context' are all shown |

## Expected Final State

'Component inventory', 'Dependency discovery', and 'Ownership context' are all shown

## Pass/Fail Criteria

**Pass:**
- All modal content matches expected values exactly
- Modal opens with background overlay

**Fail:**
- Any field missing, wrong text, or modal does not open
