---
id: ELITEA-0056
title: "Verify TOOLS section can be expanded after collapse on Pipeline Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0056: Verify TOOLS section can be expanded after collapse on Pipeline Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that after collapsing the TOOLS section on Pipeline Details, it can be re-expanded to show all content.

**Coverage:**
- Expand behavior after collapse on Pipeline Details

## Preconditions

- Logged in to {{base_url}}
- Pipeline Details page open; TOOLS section is collapsed
- Browser: Chrome (latest)

## Test Data

Any existing Pipeline with at least one tool configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline Details page and collapse the TOOLS section | TOOLS section is in collapsed state |
| 2 | Click the expand/toggle arrow next to TOOLS | TOOLS section expands |
| 3 | Verify all quick-add buttons are visible: + Toolkit, + MCP, + Agent, + Pipeline | All 4 buttons are displayed |
| 4 | Verify previously added tools are listed | All configured tools appear in the list |

## Expected Final State

All configured tools appear in the list

## Pass/Fail Criteria

**Pass:** Section expands fully; all buttons and tools are visible
**Fail:** Section does not expand or content is missing
