---
id: ELITEA-2723
title: "Malformed HTML renders with best effort"
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
- HTML file with syntax errors is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | HTML with unclosed tags, missing DOCTYPE, or invalid syntax |
| Example errors | div p text /div, missing /html, unquoted attributes |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create or locate HTML with malformed syntax | Test file is ready |
| 2 | Open the file in Preview mode | File opens in Canvas |
| 3 | Observe Preview rendering | Some content is visible |
| 4 | Verify Canvas does not crash | Canvas remains functional |
| 5 | Switch to Raw mode | Raw mode displays |
| 6 | Observe source code with errors | Source shows as-is |
| 7 | Verify user can edit the code | Editor accepts input |

## Expected Final State

- Canvas does not crash or freeze
- Preview mode renders with best-effort (browser auto-correction)
- Raw mode shows the source as-is with errors
- User can edit and fix errors in Raw mode

## Pass/Fail Criteria

**Pass:**
- Preview renders some content despite errors
- No Canvas crash or browser freeze
- Raw mode shows source as-is
- User can edit and fix errors

**Fail:**
- Canvas crashes or freezes
- No content displays at all
- Error messages block the user
- Cannot edit the file
