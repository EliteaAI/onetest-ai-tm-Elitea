---
id: ELITEA-0131
title: "Agent Publishing - Sub-Agent Version Resolution at Runtime"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: []
requirements: []
---
# ELITEA-0131: Agent Publishing - Sub-Agent Version Resolution at Runtime

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that a published agent uses the published version of its sub-agents, not the latest draft version.

## Preconditions

User logged into Elitea stage.elitea.ai\nUser has permissions to create, publish, and execute agents\nAt least one toolkit available for agent configuration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create Agent A (v1.0) with a specific prompt/instruction (e.g., 'Always respond with: Version 1 active') | Agent A created with v1.0 configuration |
| 2 | Publish Agent A as v1.0 | Agent A v1.0 is published successfully |
| 3 | Create Agent B that references Agent A as a sub-agent | Agent B created with Agent A as sub-agent |
| 4 | Publish Agent B as v1.0 | Agent B v1.0 is published successfully |
| 5 | Modify Agent A: change prompt/instruction to something different (e.g., 'Always respond with: Version 2 active') creating v2.0 as latest draft | Agent A now has v2.0 (latest) with different behavior from v1.0 |
| 6 | Execute published Agent B v1.0 with a request that triggers sub-agent invocation | Agent B uses Agent A v1.0 (published version), NOT v2.0 (latest draft) |
| 7 | Verify the response matches Agent A v1.0 behavior, not v2.0 | Response shows v1.0 behavior (e.g., 'Version 1 active'), confirming correct version resolution |
| 8 | Publish Agent A v2.0 and then execute published Agent B v1.0 again (without republishing Agent B) | Agent B v1.0 still resolves to Agent A v1.0 (the version it was published with), NOT the newly published Agent A v2.0 — version pinning is stable across sub-agent republishing |
| 9 | Republish Agent B as v2.0 (which should now pick up Agent A v2.0) and execute it | Agent B v2.0 resolves to Agent A v2.0, showing 'Version 2 active' — confirming that republishing correctly updates sub-agent version bindings |
| 10 | Delete Agent A v2.0 (revert to only v1.0 published) and attempt to execute Agent B v2.0 which references the now-deleted Agent A v2.0 | System handles the missing sub-agent version gracefully — either falls back to the latest available version with a warning, or shows a clear error message indicating the referenced version no longer exists |
| 11 | Verify the published Agent B v1.0 still works correctly after Agent A version changes (execute Agent B v1.0 one more time) | Agent B v1.0 continues to function correctly with its pinned version of Agent A, unaffected by version changes or deletions to Agent A's other versions |

## Expected Final State

Agent B v1.0 continues to function correctly with its pinned version of Agent A, unaffected by version changes or deletions to Agent A's other versions

## Pass/Fail Criteria

Published agent uses published sub-agent version, not latest
Runtime behavior matches the published version's configuration
No runtime errors when sub-agent has newer draft versions
Version resolution is deterministic
Republishing sub-agent does NOT change parent's version binding unless parent is also republished
Deleted sub-agent version produces clear error or graceful fallback
Previously published parent versions remain stable through sub-agent version lifecycle changes
