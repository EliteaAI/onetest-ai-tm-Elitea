---
id: ELITEA-0044
title: "Verify \"TOOLS\" label on Agent Details page"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0044: Verify "TOOLS" label on Agent Details page

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the section previously labeled "TOOLKITS" now displays "TOOLS" on the Agent Details page.

**Coverage:**
- Label rename from TOOLKITS → TOOLS on Agent Details
- No residual "TOOLKITS" text visible

## Preconditions

- Logged in to {{base_url}}
- At least one Agent exists in the project
- Browser: Chrome (latest)

## Test Data

Any existing Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents list page | Agents list is displayed |
| 2 | Click on any existing Agent to open Agent Details | Agent Details page opens |
| 3 | Scroll to the tools area on the right panel | The section heading reads "TOOLS" |
| 4 | Confirm no "TOOLKITS" text is present anywhere on the page | No occurrence of "TOOLKITS" is visible |

## Expected Final State

No occurrence of "TOOLKITS" is visible

## Pass/Fail Criteria

**Pass:** Section heading displays "TOOLS"; "TOOLKITS" is absent
**Fail:** Section heading still reads "TOOLKITS" or both labels appear simultaneously
