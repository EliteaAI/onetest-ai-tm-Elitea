---
id: ELITEA-2512
title: "Icon gallery pagination works correctly for uploaded skill icons"
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
- More than the default page limit of icons uploaded (e.g., 25 icons if limit is 20)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Number of Icons | >20 (or default page limit) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload more icons than the default page limit | Icons uploaded |
| 2 | Open SelectIconDialog | Dialog opens |
| 3 | Navigate to the uploaded icons section | Uploaded icons displayed |
| 4 | Verify pagination controls appear or infinite scroll triggers | Pagination/scroll available |
| 5 | Navigate through pages or scroll to load more | Additional icons load |
| 6 | Verify all uploaded icons can be accessed | All icons visible |

## Expected Final State

The uploaded icons section in SelectIconDialog paginates correctly when many icons have been uploaded.

## Pass/Fail Criteria

**Pass:**
- Pagination controls appear or infinite scroll works
- All uploaded icons accessible
- No icons missing

**Fail:**
- No pagination available
- Icons cut off or inaccessible
- Pagination errors
