---
id: ELITEA-0045
title: "Verify \"TOOLS\" label on Pipeline Details page"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0045: Verify "TOOLS" label on Pipeline Details page

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the section previously labeled "TOOLKITS" now displays "TOOLS" on the Pipeline Details page.

**Coverage:**
- Label rename on Pipeline Details page
- No residual "TOOLKITS" text

## Preconditions

- Logged in to {{base_url}}
- At least one Pipeline exists in the project
- Browser: Chrome (latest)

## Test Data

Any existing Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines list page | Pipelines list is displayed |
| 2 | Click on any existing Pipeline to open Pipeline Details | Pipeline Details page opens |
| 3 | Scroll to the tools area on the right panel | The section heading reads "TOOLS" |
| 4 | Confirm no "TOOLKITS" text is present anywhere on the page | No occurrence of "TOOLKITS" is visible |

## Expected Final State

No occurrence of "TOOLKITS" is visible

## Pass/Fail Criteria

**Pass:** Section heading displays "TOOLS"; "TOOLKITS" is absent
**Fail:** Section heading still reads "TOOLKITS" or both labels appear simultaneously
