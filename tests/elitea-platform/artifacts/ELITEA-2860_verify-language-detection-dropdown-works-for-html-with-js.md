---
id: ELITEA-2860
title: "Verify language detection dropdown still works for HTML files with JS content"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, comm:feedback, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6176]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A JS-containing HTML file exists in an artifact bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | Any JS-containing HTML file |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the file in canvas and switch to Raw mode | Raw mode shows source |
| 2 | Observe the language dropdown | Shows "HTML" as the detected language |
| 3 | Change the dropdown to "JavaScript" | Syntax highlighting updates accordingly |
| 4 | Change back to "HTML" | HTML highlighting is restored |

## Expected Final State

Automatic and manual language detection continue to function correctly for JS-containing HTML files.

## Pass/Fail Criteria

**Pass:**
- Auto-detection shows HTML; manual override updates highlighting correctly in both directions

**Fail:**
- Detected language is wrong, or manual override does not change highlighting
