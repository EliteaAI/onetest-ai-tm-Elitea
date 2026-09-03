---
id: ELITEA-3153
title: "Verify HTML file with <style> and <script> both render correctly"
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
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| File | `styled-interactive.html` — contains both `<style>` and `<script>` (script changes element color on click) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `styled-interactive.html` and open in Preview mode | Page renders with styles applied |
| 2 | Observe visual styling | Styles from `<style>` block are applied |
| 3 | Interact with the JS-driven element (click the button) | Element color changes per script logic |
| 4 | Confirm combined behavior | Both style and JS behavior work together |

## Expected Final State

Inline CSS and inline JS coexist without conflict in a single rendered document.

## Pass/Fail Criteria

**Pass:**
- Styles render correctly and JS-driven interaction works as expected

**Fail:**
- Styles are not applied, or JS interaction fails/breaks styling
