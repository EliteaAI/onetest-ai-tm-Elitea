---
id: ELITEA-2220
title: "Publish agent with sub-agent skills"
priority: critical
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
- Parent agent created with valid configuration
- Sub-agent "Helper Agent" created with 2 Skills: "Debug Skill", "Logging Skill"
- Sub-sub-agent "Nested Helper" created with 1 Skill: "Trace Skill" (2 levels deep)
- All Skills have valid content (100+ chars, no placeholders, no secrets)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Parent Agent | "Orchestrator" - no Skills attached directly |
| Sub-agent (Level 1) | "Helper Agent" with 2 Skills |
| Sub-agent Skill 1 | "Debug Skill" - debugging instructions |
| Sub-agent Skill 2 | "Logging Skill" - logging guidelines |
| Sub-sub-agent (Level 2) | "Nested Helper" with 1 Skill |
| Sub-sub-agent Skill | "Trace Skill" - tracing instructions |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open parent agent "Orchestrator" | Agent configuration loads |
| 2 | Verify sub-agent section shows "Helper Agent" attached | Sub-agent visible in configuration |
| 3 | Open "Helper Agent" in separate tab | Sub-agent loads with 2 Skills in SKILLS section |
| 4 | Verify "Helper Agent" has sub-sub-agent "Nested Helper" | Nested sub-agent visible |
| 5 | Open "Nested Helper" | Shows 1 Skill: "Trace Skill" |
| 6 | Return to parent "Orchestrator" | Parent agent active |
| 7 | Click ⋮ menu → **Publish** | Publish wizard opens |
| 8 | Complete Preparation step (version, category, terms agreement) | Continue to Validation |
| 9 | Wait for validation to complete | Result: PASS |
| 10 | Verify validation includes sub-agent Skills | No critical issues for sub-agent Skills |
| 11 | If any finding in sub-agent's Skill, verify context shows path | Context format: `sub-agent: Helper Agent > skill: Debug Skill` or similar |
| 12 | Click **Publish** | "The agent has been published" toast |
| 13 | Navigate to **Agent Hub** | Hub loads |
| 14 | Find and open published "Orchestrator" | Agent preview/detail opens |
| 15 | Add to conversation and test | Agent works |
| 16 | Send prompt that should trigger sub-agent with Skill behavior | Sub-agent's Skill instructions affect response |
| 17 | Test prompt triggering nested sub-sub-agent Skill | Nested Skill also functional |
| 18 | Search Agent Hub for "Debug Skill" | **No Skill appears as independent entity** |
| 19 | Search Agent Hub for "Trace Skill" | **No Skill appears as independent entity** |

## Expected Final State

Parent agent is published with all sub-agent and sub-sub-agent Skills embedded in the snapshot. All nested Skills are functional but not discoverable as independent entities in Agent Hub.

## Pass/Fail Criteria

**Pass:**
- Sub-agent's Skills (Level 1) embedded in parent's published snapshot
- Sub-sub-agent's Skills (Level 2) also embedded in parent's published snapshot
- Validation findings for sub-agent Skills show proper attribution with context path
- Sub-agent Skills NOT discoverable as independent entities in Agent Hub
- Published parent agent retains full nested Skill functionality

**Fail:**
- Sub-agent Skills missing from published snapshot
- Nested Skills not functional in published agent
- Skills appear as independent entities in Agent Hub
- Validation findings lack proper attribution
