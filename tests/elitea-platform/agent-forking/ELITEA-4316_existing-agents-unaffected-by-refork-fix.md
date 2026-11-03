---
id: ELITEA-4316
title: "Existing published agents remain functional after re-fork fix"
priority: medium
type: regression
module: agent-forking
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.8, eng:backend, bug]
requirements: [EliteaAI/elitea_issues#6905]
---

## Preconditions

- Published agents and existing forks exist in the system before the fix is deployed
- User has documented IDs and state of published agents and forks

## Test Data

| Field | Value |
|-------|-------|
| Published Agent IDs | Pre-fix IDs documented |
| Existing Fork IDs | Pre-fix fork IDs documented |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | (Pre-fix) Document published agent ID and existing fork IDs | IDs recorded |
| 2 | Deploy the re-fork fix to production/staging | Fix deployed successfully |
| 3 | Clear cache and reload Catalog | Published agents visible |
| 4 | Verify documented published agent still appears | Published agent accessible with same ID |
| 5 | Open the published agent | Agent details load correctly; all data intact |
| 6 | Navigate to projects with existing forks | Projects load |
| 7 | Verify existing forks still appear with same IDs | Forks accessible and unchanged |
| 8 | Open each existing fork | Fork details load correctly; all data intact |
| 9 | Attempt to execute existing forks | Forks execute without errors |
| 10 | Attempt to edit existing forks | Forks can be edited and saved |
| 11 | Fork the published agent again | New fork attempt succeeds (fix validation) |
| 12 | Verify existing forks remain unmodified | Previous forks unchanged after new fork operation |

## Expected Final State

- All pre-fix published agents and forks remain functional
- No data corruption or unexpected changes
- New fork operations work correctly after fix deployment
- No regression in existing functionality

## Pass/Fail Criteria

**Pass:**
- Published agents and existing forks accessible with same IDs
- All pre-fix agents/forks load correctly and can be executed/edited
- New fork operations succeed after fix
- No regression detected

**Fail:**
- Published agents or existing forks become inaccessible
- Any pre-fix agent/fork data corrupted or lost
- Existing forks cannot be executed or edited
- New fork operations still fail after fix
