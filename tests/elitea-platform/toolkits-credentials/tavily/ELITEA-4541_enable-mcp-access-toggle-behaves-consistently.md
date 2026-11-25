---
id: ELITEA-4541
title: "Verify the Enable MCP access for selected tools toggle behaves consistently on the Tavily toolkit"
priority: medium
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A Tavily toolkit; another toolkit type (e.g. GitHub) available for comparison

## Test Data

| Field | Value |
|-------|-------|
| Toggle | "Enable MCP access for selected tools" (default off) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Tavily toolkit form and locate the toggle | Present, default off |
| 2 | Toggle it on and save | Toolkit saves without error |
| 3 | Open an unrelated toolkit type (e.g. GitHub) | Same toggle exists with the same default/behavior |
| 4 | Toggle it back off on the Tavily toolkit and save | Change persists correctly |

## Expected Final State

The MCP access toggle on the Tavily toolkit behaves identically to other toolkit types.

## Pass/Fail Criteria

**Pass:**
- Toggle saves correctly in both states
- Behavior matches other toolkit types

**Fail:**
- The toggle fails to save
- It behaves differently than on other toolkit types
