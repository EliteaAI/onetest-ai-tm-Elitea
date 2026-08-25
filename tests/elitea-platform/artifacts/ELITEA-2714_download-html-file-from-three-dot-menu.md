---
id: ELITEA-2714
title: "Download HTML file from three-dot menu"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file is open in Canvas

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_2_between_1_3mb_structured.htm |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas | File is displayed in Canvas |
| 2 | Click three-dot menu in top-right corner | Menu dropdown appears |
| 3 | Click "Download" option | Download initiates |
| 4 | Check browser downloads folder/panel | File appears in downloads |
| 5 | Verify downloaded file name | File has correct name with .html or .htm extension |
| 6 | Open downloaded file in a web browser | File opens locally |
| 7 | Verify content renders correctly | HTML displays properly in browser |

## Expected Final State

- File is downloaded to local machine
- Downloaded file has correct name and extension
- File renders correctly when opened in a browser

## Pass/Fail Criteria

**Pass:**
- Download option initiates file download
- Downloaded file has correct filename and extension
- File renders correctly in local browser

**Fail:**
- Download fails or shows error
- File has incorrect name or no extension
- File does not render properly in browser
