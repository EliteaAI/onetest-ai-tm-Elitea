---
id: ELITEA-2511
title: "Icon picker tooltip displays correct file size and format guidance"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Expected Tooltip | "Upload a bmp, ico, gif, jpeg, jpg, png, tiff or webp image (less than 500KB)" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open SelectIconDialog from a Skill form | Dialog opens |
| 2 | Hover over or focus on the upload button/area | Tooltip appears |
| 3 | Verify tooltip text contains accepted formats | Formats listed |
| 4 | Verify tooltip text contains 500 KB size limit | Size limit mentioned |

## Expected Final State

The icon upload area displays a tooltip or helper text with correct accepted formats and file size limit.

## Pass/Fail Criteria

**Pass:**
- Tooltip displays on hover/focus
- Accepted formats listed correctly
- 500 KB limit mentioned

**Fail:**
- No tooltip displayed
- Incorrect formats listed
- Size limit missing or incorrect
