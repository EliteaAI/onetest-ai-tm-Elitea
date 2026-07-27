---
id: ELITEA-2502
title: "File size validation rejects images larger than 500kb"
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
- User has an image file larger than 500 KB prepared

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Oversized File | `.png` image file, ~600 KB |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Prepare an image file larger than 500 KB (e.g., 600 KB `.png`) | File ready |
| 2 | Open the Skill create or edit form | Form loads |
| 3 | Click on the icon picker to open SelectIconDialog | Dialog opens |
| 4 | Attempt to upload the oversized file | Upload attempted |
| 5 | Verify an error message is displayed indicating file exceeds size limit | Error message shown (e.g., "File size exceeds 500 KB limit") |
| 6 | Verify the file is NOT uploaded to the gallery | File not in gallery |
| 7 | Verify the Skill's icon remains unchanged | Original icon (default or previous) retained |

## Expected Final State

Uploading an image larger than 500 KB is rejected with a clear error message, and no changes occur to the Skill's icon.

## Pass/Fail Criteria

**Pass:**
- Error message displayed for oversized file
- File not added to gallery
- Skill icon unchanged

**Fail:**
- Oversized file uploads successfully
- No error message shown
- Skill icon changes despite error
