---
id: ELITEA-4550
title: "Sub-agent Web Search access depends only on its own toggle, never inherited from parent"
priority: critical
type: functional
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- An agent with at least one nested sub-agent is configured

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Delegation prompt | "Ask the sub-agent to find today's top news on [topic]" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set parent agent Web Search = enabled, sub-agent Web Search = disabled. Run parent via test chat with the delegation prompt | Sub-agent does not perform a web search |
| 2 | Set parent agent Web Search = disabled, sub-agent Web Search = enabled. Repeat the delegation test | Sub-agent CAN perform a web search even though the parent cannot |
| 3 | Set both parent and sub-agent Web Search = enabled. Repeat the delegation test | Both can independently use Web Search |
| 4 | Set both parent and sub-agent Web Search = disabled. Repeat the delegation test | Neither uses Web Search |

## Expected Final State

Sub-agent Web Search availability tracks only its own version's toggle in all four combinations.

## Pass/Fail Criteria

**Pass:**
- All four combinations behave exactly as described, with no inheritance from the parent's toggle

**Fail:**
- Sub-agent behavior in any combination is determined by the parent's toggle instead of its own
