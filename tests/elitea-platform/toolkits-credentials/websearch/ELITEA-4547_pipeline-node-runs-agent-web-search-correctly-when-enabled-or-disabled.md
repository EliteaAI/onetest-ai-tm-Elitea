---
id: ELITEA-4547
title: "Pipeline node runs agent Web Search correctly when enabled or disabled on the agent"
priority: critical
type: integration
module: web-search
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

## Preconditions

- User is logged in to `{{base_url}}`
- A pipeline exists containing a node that invokes an agent/agent version
- Web Search is available for the project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Node prompt | "Find today's top news on [topic]" |
| Trigger types to test | Manual run, REST trigger, webhook, scheduled run (if configurable) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open/build a pipeline with a node running an agent version with Web Search **enabled** | Node configuration saves |
| 2 | Run the pipeline with the test node prompt | Node output includes search-derived content with markdown-link citations; pipeline completes successfully end to end |
| 3 | Change the node's agent version (or duplicate the node) to one with Web Search **disabled**; run again with the same prompt | No web search occurs; pipeline still completes normally without errors |
| 4 | Trigger the enabled-node pipeline via each available entry point: manual run, REST trigger, webhook, scheduled run (if configurable) | Web search behaves identically (searches) regardless of trigger source |
| 5 | Trigger the disabled-node pipeline via the same entry points | No web search occurs for any trigger source |

## Expected Final State

Pipeline Web Search behavior is driven solely by the invoked agent version's own toggle, consistently across every trigger source.

## Pass/Fail Criteria

**Pass:**
- Enabled node searches and cites sources via every trigger type; disabled node never searches via any trigger type; pipeline always completes

**Fail:**
- Search behavior is inconsistent across trigger types, or the pipeline run fails/halts unexpectedly
