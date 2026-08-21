---
id: ELITEA-2691
title: "Unavailable Tools Render in Separate Block Above Grouped Tools"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, unavailable, deprecated]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2691: Unavailable Tools Render in Separate Block Above Grouped Tools

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that selected tools which are no longer available appear in a dedicated "Unavailable" section above the tool groups with appropriate warnings.

**Coverage:**
- Unavailable tools section appears above grouped tools
- Unavailable tools display with warning styling
- "Tool is not available" tooltip shown on hover
- Unavailable tools can be deselected
- Search filtering does not hide the unavailable tools section

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- A toolkit exists with at least one tool that was previously selected but is now unavailable/deprecated
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit that has unavailable/deprecated tools. | Toolkit configuration opens. |
| 2 | Navigate to Tools section. | Tools section is visible. |
| 3 | Verify an "Unavailable" block appears above the Read/Create & update/Delete/Execute groups. | **"Unavailable"** section is displayed **above** the tool groups. |
| 4 | Verify unavailable tools are displayed within this block. | Unavailable tools are listed inside the "Unavailable" section. |
| 5 | Verify unavailable tools have distinct warning styling (different from normal tools). | Unavailable tools have **warning styling** (e.g., muted color, warning icon). |
| 6 | Hover over an unavailable tool. | **"Tool is not available"** tooltip appears. |
| 7 | Click on an unavailable tool to deselect it. | Unavailable tool becomes **deselected**. And disapear from list (including respective section Read/Create & update etc.)|
| 8 | Type a search term in the search field (e.g., "read"). | Search filters only available tools. |
| 9 | Verify the unavailable tools block is NOT affected by search filtering. | Unavailable tools section **remains visible** regardless of search term. |
| 10 | Clear search and verify unavailable block is still present. | Unavailable section is still visible. |

## Expected Final State

Unavailable tools section displays correctly and is not affected by search filtering.

## Pass/Fail Criteria

**Pass:**
- Unavailable tools section appears above grouped tools
- Unavailable tools display with warning styling
- "Tool is not available" tooltip shown on hover
- Unavailable tools can be deselected
- Search filtering does not hide the unavailable tools section

**Fail:**
- Unavailable tools are mixed with available tools in groups
- No warning styling on unavailable tools
- Tooltip is missing on unavailable tools
- Unavailable tools cannot be deselected
- Search filtering hides the unavailable tools section
