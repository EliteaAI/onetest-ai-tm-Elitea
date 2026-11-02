---
id: ELITEA-4313
title: "Forked agent can be published to Catalog independently"
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
- A forked agent exists in target project (from ELITEA-4307)

## Test Data

| Field | Value |
|-------|-------|
| Forked Agent | Agent created in testproj1 from published original |
| Base URL | `{{base_url}}/app/` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to target project (testproj1) | Project loads |
| 2 | Open the forked agent | Agent details displayed |
| 3 | Locate and click Publish to Catalog button | Publish dialog appears |
| 4 | Complete publish workflow (provide required metadata) | Publish request submitted |
| 5 | Verify publish succeeds | HTTP 200 response; success confirmation shown |
| 6 | Navigate to Catalog/Agent Hub | Catalog loads |
| 7 | Search for or locate the newly published agent | Forked agent appears as separate published entry in Catalog |
| 8 | Verify new published entry has distinct ID | Published entry ID differs from original published agent ID |
| 9 | Inspect new published entry's metadata | Has own shared_owner_id and shared_id distinct from original published agent |
| 10 | Verify new published agent can be forked | Fork button functional on newly published entry |

## Expected Final State

- Forked agent successfully published to Catalog as independent entry
- New published version has distinct shared metadata from original published agent
- Forked agent continues to work in original project

## Pass/Fail Criteria

**Pass:**
- Publish operation succeeds with HTTP 200
- New published agent appears in Catalog with unique ID
- shared_owner_id and shared_id are distinct from original
- Newly published agent can be forked

**Fail:**
- Publish fails with error
- Agent does not appear in Catalog after publish
- New published entry shares ID with original published agent
- New published agent cannot be forked
