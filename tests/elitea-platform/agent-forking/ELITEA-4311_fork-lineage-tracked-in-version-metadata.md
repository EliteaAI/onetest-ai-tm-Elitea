---
id: ELITEA-4311
title: "Fork lineage correctly recorded in version metadata"
priority: critical
type: functional
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- User is logged into `{{base_url}}`
- A published agent has been forked into target project (from ELITEA-4307)

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Agent used in ELITEA-4307 |
| Forked Agent | Copy created in target project |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to target project | Project loads |
| 2 | Open the forked agent | Agent details displayed |
| 3 | Navigate to Version History or Metadata section | Version list displayed with ancestry information |
| 4 | Inspect the version metadata | Version record shows parent fork information |
| 5 | Verify parent_agent_id field | Contains ID of published agent (fork source) |
| 6 | Verify parent_version_id field | Contains version ID from published agent |
| 7 | Verify fork_source indicator | Metadata indicates this agent is a fork |
| 8 | Perform second fork of same published agent to same project (ELITEA-4308 scenario) | Second fork created |
| 9 | Open the second forked agent | Agent details displayed |
| 10 | Inspect version metadata of second fork | Parent information present and distinct from first fork |
| 11 | Verify both forks have separate lineage records | Each fork's metadata is independent; not overwritten |

## Expected Final State

- Fork lineage metadata correctly recorded for each fork
- Parent agent and version information traceable
- Multiple forks have separate, non-conflicting lineage records

## Pass/Fail Criteria

**Pass:**
- Version metadata contains valid parent fork information
- Multiple forks have distinct lineage records
- Parent agent ID matches published agent ID

**Fail:**
- Lineage metadata missing or NULL
- Lineage metadata overwritten by subsequent forks
- Parent information points to wrong agent
