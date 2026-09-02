---
id: ELITEA-2876
title: "Verify AI-generated HTML saved to artifacts executes JS in Preview mode"
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
- User has access to a Chat conversation and an artifact bucket

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test files repository | `https://epam.sharepoint.com/:f:/r/sites/EPAMAlita_test_sam/Shared%20Documents/Test_Chornyi/6176-html-js-test-files` |
| Prompt | "Create an HTML file that displays today's date using JavaScript" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In a chat conversation, prompt the assistant to generate the HTML file | Assistant generates an HTML file with an inline script |
| 2 | Save the generated HTML to an artifact bucket | File saves successfully |
| 3 | Navigate to Artifacts and open the saved file in Preview mode | JS runs and the date is displayed |
| 4 | Compare behavior to a manually uploaded HTML file | Behaves identically |

## Expected Final State

AI-generated HTML files saved to Artifacts support inline JS execution identically to manually uploaded files.

## Pass/Fail Criteria

**Pass:**
- JS executes correctly and the date renders after saving to Artifacts

**Fail:**
- JS fails to execute for the AI-generated file despite working for manually uploaded files
