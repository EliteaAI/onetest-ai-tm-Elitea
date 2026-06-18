---
id: ELITEA-0051
title: "Verify TOOLS section can be collapsed on Agent Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0051: Verify TOOLS section can be collapsed on Agent Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TOOLS section on the Agent Details page can be collapsed (minimized) using the toggle control.

**Coverage:**
- Collapse behavior of TOOLS section on Agent Details

## Preconditions

- Logged in to {{base_url}}
- At least one Agent exists
- TOOLS section is in expanded state
- Browser: Chrome (latest)

## Test Data

Any existing Agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent Details page | Agent Details page is displayed |
| 2 | Confirm TOOLS section is expanded | TOOLS section content (buttons and tools) is visible |
| 3 | Click the collapse/toggle arrow (>) next to TOOLS | TOOLS section collapses; content is hidden |
| 4 | Verify the "TOOLS" label is still visible in the collapsed state | "TOOLS" label remains visible; section content is hidden |

## Expected Final State

"TOOLS" label remains visible; section content is hidden

## Pass/Fail Criteria

**Pass:** TOOLS section collapses; label remains; content is hidden
**Fail:** Section does not collapse or the label disappears on collapse
