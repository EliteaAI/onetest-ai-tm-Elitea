---
id: ELITEA-2575
title: "Execute tool with pagination parameters"
priority: medium
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p2]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2575: Execute tool with pagination parameters

**Module:** Toolkits · **Priority:** Medium · **Type:** Functional

**Objective:** Verify pagination works correctly across multiple pages

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- Toolkit is configured
- Tool supports pagination

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/
- Pagination parameters: page=1, per_page=10

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Select tool with pagination support | First page returns 10 results |
| 2 | Provide parameters: page=1, per_page=10 | Second page returns next 10 results |
| 3 | Execute tool | No overlap between pages |
| 4 | Note results | Results are correctly paginated |
| 5 | Change to page=2 | Page 2 loads successfully |
| 6 | Execute again | Different results from page 1 |
| 7 | Compare results | Pagination works correctly |

## Expected Final State

First page returns 10 results, second page returns next 10 results with no overlap between pages.

## Pass/Fail Criteria

**Pass:**
- First page returns 10 results
- Second page returns next 10 results
- No overlap between pages

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
