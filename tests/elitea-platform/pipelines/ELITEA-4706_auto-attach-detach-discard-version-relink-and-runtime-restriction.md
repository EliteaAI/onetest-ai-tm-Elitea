---
id: ELITEA-4706
title: "Tools in Nodes — Auto-attach, Detach, Discard, Version Re-link and Runtime Tool Restriction"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7159]
---
# ELITEA-4706: Tools in Nodes — Auto-attach, Detach, Discard, Version Re-link and Runtime Tool Restriction

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that picking an item inside a node auto-attaches it to the pipeline version (one attachment per item), that removing it from the last node (or deleting that node) detaches it, that attach/detach are unsaved changes reverted by Discard, that Agent version changes re-link the attachment, and that the LLM only gets its selected tools at runtime.

**Coverage:**
- Auto-attach on pick (Agent, LLM, MCP, Toolkit)
- One attachment for an item used by several nodes; existing tool restrictions reused
- Detach on X-clear from the last node or on node deletion
- Attach and detach are unsaved changes; Discard reverts both directions
- Show tools reflects selected tools
- Agent Version change re-links; run uses the new version
- LLM runtime tool restriction
- Save errors are explicit (no silent partial save)
- New unsaved pipeline attaches correctly once saved
- See ELITEA-4718 for the main flow

## Preconditions

- Logged in to {{base_url}}
- Project with: a toolkit (several tools), an MCP, an agent with 2 versions

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In a saved pipeline, add a Toolkit node and pick the toolkit + a tool. | The toolkit appears in the left TOOLS section automatically; Save and Discard become enabled. |
| 2 | Repeat step 1 with an Agent node, an MCP node and an LLM node (Toolkits & MCPs). | Each picked item appears in TOOLS automatically. |
| 3 | In a second node, pick the same toolkit. | TOOLS still has **one** entry for it; Used by lists both nodes; existing tool restrictions are reused. |
| 4 | Expand **Show tools** on the toolkit in TOOLS; add/remove a tool in a node. | Selected tools are listed and update when tools are added/removed in the node. |
| 5 | Save. Click the ✕ (clear) next to the toolkit in one node. | Entry remains (still used by the other node). |
| 6 | Click ✕ in the last node using it. | Entry disappears from TOOLS; **Discard becomes enabled**. |
| 7 | Click **Discard**. | The toolkit is restored on the node(s) and in TOOLS (unsaved detach reverted). |
| 8 | Pick a new MCP in a node (unsaved), click **Discard**. | The MCP is removed from the node and from TOOLS (unsaved attach reverted). |
| 9 | Delete the last node using an item, then Save. | The item is detached from TOOLS. |
| 10 | In the Agent node, change **Version** to the other version; Save; run. | The pipeline runs with the newly selected version. |
| 11 | In the LLM node select only one tool of a toolkit; run with a prompt that needs a different tool. | The LLM only has access to the selected tool. |
| 12 | Create a brand-new pipeline; add a Toolkit node and pick a toolkit before the first save; Save. | The toolkit is attached correctly after the first save. |
| 13 | Observe save behaviour throughout. | No silent partial saves; any attach/detach failure shows a clear error. |

## Expected Final State

Items picked in nodes are attached once and detached when no node uses them; attach/detach behave as unsaved changes; version and tool restrictions are honored at runtime.

## Pass/Fail Criteria

**Pass:**
- Auto-attach on pick; single attachment for shared items
- Detach on last X-clear or node deletion
- Discard reverts both attach and detach
- Version re-link and LLM tool restriction honored at runtime

**Fail:**
- Duplicate attachments, or item remains after the last node stops using it
- Discard does not revert attach/detach
- Run uses the old version or tools outside the selection
