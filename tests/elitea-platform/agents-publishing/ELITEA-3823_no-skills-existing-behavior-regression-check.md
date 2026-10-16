---
id: ELITEA-3823
title: "No skills - existing behavior regression check"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:skills, feat:agent-publishing, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5803]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has editor/admin role with `models.applications.publish.post` permission
- Test agent with sub-agent (both without Skills)
- Agent has internal tools only (no external toolkits/MCPs attached)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent Name | "Regression Test Agent" |
| Skills Attached | 0 (none) |
| Sub-agent | "Plain Helper" (also 0 Skills) |
| Tools | Internal tools only (no external toolkits/MCPs) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open agent with sub-agent (both without Skills) | Agent loads |
| 2 | Verify internal tools attached (no external toolkits/MCPs) | Internal tools visible in configuration |
| 3 | Click ⋮ menu → **Publish** → complete full flow | Agent published |
| 4 | Add published agent to conversation | Agent ready |
| 5 | Verify sub-agent embedded in snapshot | Sub-agent works in published version |
| 6 | Verify internal tools retained | Internal tools functional |
| 7 | Click ⋮ menu → **Unpublish** | Agent unpublished |
| 8 | Verify draft version intact | All configuration preserved |
| 9 | Re-publish the agent | Publishes again successfully |
| 10 | Verify consistent behavior | Same as before Skills enhancement |

## Expected Final State

Existing agent publishing behavior (sub-agent embedding, internal tools retention, unpublish/re-publish) remains unchanged for agents without Skills. Full backward compatibility confirmed.

## Pass/Fail Criteria

**Pass:**
- Sub-agent embedding unchanged
- Internal tools retention unchanged
- Unpublish/re-publish behavior unchanged
- Full backward compatibility confirmed

**Fail:**
- Sub-agent not embedded correctly
- Internal tools missing or broken
- Unpublish/re-publish behavior changed
