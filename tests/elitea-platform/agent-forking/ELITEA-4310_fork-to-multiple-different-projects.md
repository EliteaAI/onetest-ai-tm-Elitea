---
id: ELITEA-4310
title: "Fork same published agent to multiple different projects"
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
- At least one published agent exists in Catalog
- At least two different target projects available (testproj1, testproj2)

## Test Data

| Field | Value |
|-------|-------|
| Published Agent | Any published agent |
| Target Projects | testproj1, testproj2 |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Catalog/Agent Hub | Catalog loads; published agents visible |
| 2 | Select a published agent | Agent details displayed |
| 3 | Click Fork button | Fork dialog appears |
| 4 | Select testproj1 from dropdown | Target project shown |
| 5 | Click Confirm | Fork to testproj1 succeeds (HTTP 200) |
| 6 | Navigate to Catalog/Agent Hub | Catalog reloaded |
| 7 | Select the same published agent again | Agent details displayed |
| 8 | Click Fork button | Fork dialog appears |
| 9 | Select testproj2 from dropdown | Target project shown |
| 10 | Click Confirm | Fork to testproj2 succeeds (HTTP 200) |
| 11 | Navigate to testproj1 | Project loads; verify forked agent present with unique ID |
| 12 | Navigate to testproj2 | Project loads; verify forked agent present with unique ID |
| 13 | Verify both forks have different IDs | Agent IDs in testproj1 and testproj2 are distinct |
| 14 | Verify both have separate version histories | Each fork has independent version lineage |

## Expected Final State

- Published agent is forked into both testproj1 and testproj2
- Each fork has unique ID and separate metadata
- Each fork has independent version history

## Pass/Fail Criteria

**Pass:**
- Both forks succeed with HTTP 200
- Each project contains the forked agent with unique ID
- Version histories are independent

**Fail:**
- Either fork fails with error
- Forked agents have same ID
- Version histories are shared or corrupted
