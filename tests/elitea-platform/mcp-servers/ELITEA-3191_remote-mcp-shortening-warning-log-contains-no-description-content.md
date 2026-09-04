---
id: ELITEA-3191
title: "Remote MCP: warning log emitted on description shortening contains only tool name and lengths, no description content"
priority: low
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3191: Shortening Warning Log Has No Content Leak

**Module:** Mcp Servers · **Priority:** Low · **Type:** Functional

**Objective:** Verify that when a tool's description is shortened due to a configured cap, the resulting warning log entry identifies the tool and reports old/new lengths only — it must not include the actual description text (a potential content/privacy leak into logs).

## Preconditions

- User is logged into Elitea platform
- Access to application/service logs or traces for the Remote MCP toolkit's backend (dev/QA log access)
- A Remote MCP toolkit configured with a cap that will cause at least one tool's description to be shortened

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Configure a cap on the Remote MCP toolkit that is smaller than at least one tool's description | Value saved |
| 2 | Trigger tool discovery so shortening occurs | Tools reload; shortened description observed as in ELITEA-3184 |
| 3 | Locate the corresponding warning log entry for this event | A warning log line is present referencing the tool |
| 4 | Inspect the log line's content | Contains the tool name and the old/new description lengths (numbers) only |
| 5 | Search the log line for any excerpt of the actual description text | No description text/content is present in the log line |

## Expected Final State

Shortening events are observable in logs for diagnostics, without leaking any of the underlying (potentially sensitive) description content.

## Pass/Fail Criteria

**Pass:** Warning log contains tool name and lengths only, no description text.
**Fail:** Warning log includes any portion of the actual description content.
