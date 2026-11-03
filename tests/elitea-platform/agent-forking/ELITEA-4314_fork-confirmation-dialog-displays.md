---
id: ELITEA-4314
title: "Fork confirmation dialog displays and accepts user input"
priority: medium
type: functional
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- At least one published agent exists in Catalog
- At least one target project available

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Any published agent in Catalog |
| Target Project | testproj1 (or any available project) |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog/Agent Hub | Catalog loads; published agents visible |
| 2 | Select a published agent | Agent details displayed |
| 3 | Click Fork button | Fork dialog modal appears on screen |
| 4 | Verify dialog displays project selector | Dropdown with available projects shown |
| 5 | Select target project from dropdown | Selected project name displayed in dialog |
| 6 | Verify Confirm button present | Confirm button visible and clickable |
| 7 | Verify Cancel button present | Cancel button visible and clickable |
| 8 | Click Confirm button | Dialog closes; fork operation begins |
| 9 | Wait for fork completion | Fork succeeds; user navigated to target project or success shown |
| 10 | Repeat steps 2-3, then click Cancel | Dialog appears |
| 11 | Click Cancel button | Dialog closes without executing fork |
| 12 | Verify no fork was created | Target project agent list unchanged |

## Expected Final State

- Fork dialog displays correctly before fork execution
- User can select target project and confirm or cancel
- Confirm triggers fork; Cancel closes dialog without action

## Pass/Fail Criteria

**Pass:**
- Dialog appears with project selector and action buttons
- Selected project displayed correctly
- Confirm triggers fork; Cancel aborts without creating fork
- UI responds correctly to user input

**Fail:**
- Dialog fails to appear
- Project selector missing or non-functional
- Action buttons missing or non-functional
- Confirm/Cancel behavior incorrect
