---
id: ELITEA-2720
title: "HTML with images renders images correctly"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file containing image tags is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | HTML file with img tags (embedded base64 or external URLs) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate HTML file with img tags | Test file is ready |
| 2 | Open the file in Preview mode | HTML renders in Canvas |
| 3 | Observe image rendering for valid URLs | Images display correctly |
| 4 | Verify image positioning matches HTML/CSS | Layout is correct |
| 5 | Verify image sizing matches definitions | Dimensions are correct |
| 6 | If file contains broken image URLs, observe behavior | Broken image indicator shows |

## Expected Final State

- Images with valid URLs/sources display correctly
- Image positioning and sizing match HTML/CSS definitions
- Broken image URLs show appropriate placeholder or icon

## Pass/Fail Criteria

**Pass:**
- Valid images display correctly in Preview
- Image positioning matches HTML/CSS
- Broken URLs show placeholder/broken image icon

**Fail:**
- Valid images do not display
- Image positioning or sizing is wrong
- Broken URLs cause errors or crash
