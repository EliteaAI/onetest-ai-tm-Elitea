---
id: ELITEA-2863
title: "Verify HTML file with a single tag opens correctly"
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
- An artifact bucket exists and is available for file upload

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| File | `single-tag.html` — contains only `<p>Hello from single tag</p>` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload `single-tag.html` and open in Preview mode | Paragraph text is visible |
| 2 | Check for errors | No error banner or parse error is shown |

## Expected Final State

A minimal HTML file without `<html>`/`<head>`/`<body>` wrappers still renders correctly.

## Pass/Fail Criteria

**Pass:**
- Text renders correctly with no errors

**Fail:**
- File fails to open, renders blank, or shows a parse error
