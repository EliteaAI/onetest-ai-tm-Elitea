---
id: ELITEA-0053
title: "Verify TOOLS section can be collapsed on Pipeline Details"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, pipeline, 5117]
requirements: [EliteaAI/elitea_issues#5117]
---
# ELITEA-0053: Verify TOOLS section can be collapsed on Pipeline Details

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TOOLS section on the Pipeline Details page can be collapsed using the toggle control.

**Coverage:**
- Collapse behavior of TOOLS section on Pipeline Details

## Preconditions

- Logged in to {{base_url}}
- At least one Pipeline exists
- TOOLS section is in expanded state
- Browser: Chrome (latest)

## Test Data

Any existing Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Pipeline Details page | Pipeline Details page is displayed |
| 2 | Confirm TOOLS section is expanded | TOOLS section content is visible |
| 3 | Click the collapse/toggle arrow (>) next to TOOLS | TOOLS section collapses; content is hidden |
| 4 | Verify the "TOOLS" label is still visible in the collapsed state | "TOOLS" label remains; content hidden |

## Expected Final State

"TOOLS" label remains; content hidden

## Pass/Fail Criteria

**Pass:** TOOLS section collapses; label remains visible
**Fail:** Section does not collapse or label disappears
