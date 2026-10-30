---
id: ELITEA-4233
title: "Verify Project/Shared indicator is visible in light and dark themes"
priority: medium
type: functional
module: llm-selector
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is a member of Team Project A, which has both project-level and Shared LLMs

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |

Themes (run all steps once per row):

| Theme |
|-------|
| Dark |
| Light |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch the application to the theme from the Test Data row | The theme is applied across the UI |
| 2 | Open a conversation in Chats and open the LLM model dropdown | The dropdown opens |
| 3 | Inspect a project-level model entry | The Project indicator is clearly visible with sufficient contrast against the dropdown background |
| 4 | Inspect a Shared model entry | The Shared indicator is clearly visible with sufficient contrast against the dropdown background |
| 5 | Repeat steps 1–4 for the other theme | Results match steps 1–4 |

## Expected Final State

Both Project and Shared indicators are visible and legible in dark and light themes.

## Pass/Fail Criteria

**Pass:**
- Project and Shared indicators are visible and distinguishable in both themes

**Fail:**
- Either indicator is invisible, low-contrast or rendered incorrectly in either theme
