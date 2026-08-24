---
id: ELITEA-2716
title: "Switch to Raw mode shows syntax highlighting"
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
| Test file | Any HTML file from Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas | File displays in Preview mode |
| 2 | Switch to Raw mode | Raw mode displays HTML source |
| 3 | Observe HTML tags | Tags have distinct color |
| 4 | Observe attribute names | Attribute names are highlighted |
| 5 | Observe attribute values | Values have different color |
| 6 | Observe string content | Strings are colored |
| 7 | If comments are present, observe their color | Comments have distinct color |

## Expected Final State

- HTML code displays with proper syntax highlighting
- Different code elements have distinct colors
- Code is easy to read and understand

## Pass/Fail Criteria

**Pass:**
- HTML tags are colored distinctly
- Attribute names are highlighted differently from values
- String values are colored
- Syntax highlighting improves readability

**Fail:**
- No syntax highlighting (all text is same color)
- Incorrect highlighting (wrong elements colored)
- Colors make code harder to read
