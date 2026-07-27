---
id: ELITEA-2493
title: "Upload custom icon during skill creation via create skill form"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- User has access to Skills page via sidebar

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Skill Name | `test-icon-skill` |
| Icon File | Valid `.png` image file under 500 KB |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills page via sidebar | Skills page loads with card list view |
| 2 | Click **+ Create** button | New Skill creation form opens |
| 3 | Locate the icon picker element (EntityIcon component) in the form | Icon picker is visible and clickable |
| 4 | Click on the icon picker | SelectIconDialog modal opens |
| 5 | Click **Upload** button in the dialog | File picker opens |
| 6 | Select a valid `.png` image file (under 500 KB) | File is selected |
| 7 | Confirm upload | Image appears in the uploaded icons section of the dialog |
| 8 | Select the uploaded icon and close the dialog | Selected icon is displayed in the form |
| 9 | Fill in Name: `test-icon-skill`, Description, and Instructions | Fields are populated |
| 10 | Click **Save** | Skill is saved successfully |
| 11 | Verify the Skill detail page displays the custom icon | Custom icon is visible on detail page |
| 12 | Navigate to Skills list page | Skills list page loads |
| 13 | Locate the created skill card | Card displays the custom icon, not the default SVG |

## Expected Final State

A new Skill is created with a custom icon that displays correctly on both the detail page and the Skills list page card.

## Pass/Fail Criteria

**Pass:**
- Custom icon is uploaded successfully
- Custom icon displays on Skill detail page
- Custom icon displays on Skills list card

**Fail:**
- Upload fails with error
- Default SVG icon shown instead of custom icon
- Skill creation fails
