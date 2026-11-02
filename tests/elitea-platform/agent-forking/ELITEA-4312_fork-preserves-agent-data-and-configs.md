---
id: ELITEA-4312
title: "Fork preserves all agent data and configurations"
priority: high
type: functional
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- A published agent with multiple versions, custom configurations, and attached toolkits exists

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Agent with: custom name, description, system prompt, model selection, multiple toolkits, custom settings |
| Target Project | testproj1 |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Document published agent's key attributes | Name, description, system prompt, model, toolkits, settings recorded |
| 2 | Navigate to Catalog and fork the published agent to testproj1 | Fork succeeds |
| 3 | Open the forked agent in testproj1 | Agent details displayed |
| 4 | Compare agent name with published original | Names match exactly |
| 5 | Compare agent description | Descriptions match exactly |
| 6 | Compare system prompt | System prompts match exactly |
| 7 | Verify model selection | Same model selected in fork as in original |
| 8 | Verify all toolkits present | All toolkits from published agent appear in fork |
| 9 | Verify custom settings | All custom settings/configurations are identical |
| 10 | Verify version history | Version count and history present; shows fork ancestry |
| 11 | Side-by-side comparison of published vs forked agent | No missing or corrupted data detected |

## Expected Final State

- Forked agent is exact copy of published agent
- All attributes, configurations, toolkits, and metadata preserved
- Version history intact with fork lineage

## Pass/Fail Criteria

**Pass:**
- All agent attributes match between published and forked versions
- No data missing or corrupted
- Version history present and accurate
- All toolkits and settings preserved

**Fail:**
- Any attribute differs between published and fork
- Toolkits missing from fork
- Settings lost or changed
- Version history empty or incorrect
