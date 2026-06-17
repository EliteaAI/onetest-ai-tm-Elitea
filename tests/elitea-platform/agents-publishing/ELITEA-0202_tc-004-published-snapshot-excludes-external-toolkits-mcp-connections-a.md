---
id: ELITEA-0202
title: "TC-004: Published Snapshot Excludes External Toolkits, MCP Connections, and Pipelines (Including Sub-Agent's)"
priority: critical
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0202: TC-004: Published Snapshot Excludes External Toolkits, MCP Connections, and Pipelines (Including Sub-Agent's)

**Module:** Agents Publishing · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that publishing Agent B (which has an external toolkit, MCP, pipeline, and a sub-agent that also has a toolkit/MCP) produces a snapshot where all external integrations are auto-removed, the publish succeeds without error, and the source agent configuration remains unchanged.

Coverage:
- External toolkits removed from published snapshot
- MCP connections removed from published snapshot
- Pipelines removed from published snapshot
- Sub-agent's toolkits and MCPs also removed
- Source agent in project is NOT modified
- Publish completes successfully despite removals (no error)

## Preconditions

- Logged in as User A
- Agent B configured with: 1 external toolkit, 1 MCP connection, 1 pipeline reference, and 1 sub-agent that has its own toolkit + MCP
- Agent B has at least 1 saved version

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Agent B. Note the names of: external toolkit, MCP, pipeline, sub-agent's toolkit | All are visible in Agent B configuration |
| 2 | Click 'Publish' on Agent B | Publish modal opens |
| 3 | Enter 'v1.0-excl-test' in Version Name, check agreement, click Continue → wait for validation → verify 'Excluding components...' sub-text visible during loading → click Publish on validation result | Success notification appears: 'Agent published successfully' (or equivalent) |
| 4 | Navigate to Agents Studio and find published Agent B | Agent B appears in Studio listing |
| 5 | Start a new conversation with published Agent B | Conversation starts successfully |
| 6 | Ask the agent to use its external toolkit tool (e.g., call a GitHub tool) | Tool is NOT available; agent responds it cannot access that integration OR no such tool exists in this version |
| 7 | Ask the agent to use an MCP tool | MCP tool is NOT available in the published version |
| 8 | Navigate back to Agent B in the Agents project list | Agent B configuration is intact — original toolkit, MCP, and pipeline are still present |

## Expected Final State

Agent B configuration is intact — original toolkit, MCP, and pipeline are still present

## Pass/Fail Criteria

PASS:
- Publish completes with success notification
- Published agent in Studio does not expose external toolkit, MCP, or pipeline tools
- Source Agent B configuration in project is unchanged after publish
- No error message during publishing due to excluded components

FAIL:
- Publish fails with an error related to toolkit/MCP/pipeline exclusion
- External toolkit tools are still callable in the published agent conversation
- Source agent configuration is altered after publishing
