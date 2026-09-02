---
id: ELITEA-2845
title: "Verify Preview/Raw mode toggle works correctly for HTML files with JS"
priority: high
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
| File | Any JS-containing HTML file (e.g., `inline-script-basic.html`) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the file in Preview mode | Rendered/executed output is shown |
| 2 | Click the **Raw** tab | Syntax-highlighted HTML source is shown, not the rendered output |
| 3 | Edit a line in Raw mode (e.g., change a string in the script) | Edit is accepted in the editor |
| 4 | Click the **Preview** tab | Updated script output is reflected |

## Expected Final State

Toggling between Preview and Raw modes reliably reflects the current source content, including unsaved edits.

## Pass/Fail Criteria

**Pass:**
- Raw shows accurate source; Preview reflects live edits after toggling back

**Fail:**
- Preview shows stale output after an edit, or Raw/Preview content is out of sync
