---
id: ELITEA-2503
title: "File format validation accepts only allowed image types"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5699]
---

## Preconditions

- User is logged in to `{{base_url}}` as Admin or Editor role
- Test files for each format prepared

## Test Data

| File Type | Expected Result |
|-----------|-----------------|
| `.jpg` | Accepted |
| `.jpeg` | Accepted |
| `.png` | Accepted |
| `.gif` | Accepted |
| `.bmp` | Accepted |
| `.webp` | Accepted |
| `.tiff` | Accepted |
| `.ico` | Accepted |
| `.svg` | Rejected |
| `.pdf` | Rejected |
| `.txt` | Rejected |
| `.exe` | Rejected |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open SelectIconDialog from a Skill form | Dialog opens |
| 2 | Attempt to upload `.jpg` file | File accepted, appears in gallery |
| 3 | Attempt to upload `.jpeg` file | File accepted, appears in gallery |
| 4 | Attempt to upload `.png` file | File accepted, appears in gallery |
| 5 | Attempt to upload `.gif` file | File accepted, appears in gallery |
| 6 | Attempt to upload `.bmp` file | File accepted, appears in gallery |
| 7 | Attempt to upload `.webp` file | File accepted, appears in gallery |
| 8 | Attempt to upload `.tiff` file | File accepted, appears in gallery |
| 9 | Attempt to upload `.ico` file | File accepted, appears in gallery |
| 10 | Attempt to upload `.svg` file | File rejected with error or file picker does not allow selection |
| 11 | Attempt to upload `.pdf` file | File rejected |
| 12 | Attempt to upload `.txt` file | File rejected |
| 13 | Attempt to upload `.exe` file | File rejected |

## Expected Final State

Only allowed image formats (.jpg, .jpeg, .png, .gif, .bmp, .webp, .tiff, .ico) are accepted; all other formats are rejected.

## Pass/Fail Criteria

**Pass:**
- All 8 valid formats upload successfully
- All 4 invalid formats are rejected

**Fail:**
- Valid format rejected
- Invalid format accepted
