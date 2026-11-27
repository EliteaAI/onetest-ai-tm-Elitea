---
id: ELITEA-5023
title: "Explore list visibility follows permissions"
priority: critical
type: regression
module: new-sidebar
status: draft
execution_type: manual
tags: [automated:UI:regression, r-2.0.9, eng:design, nfr:ui]
requirements: [EliteaAI/elitea_issues#7564, EliteaAI/elitea_issues#7560]
---
# ELITEA-5023: Explore list visibility follows permissions

## Preconditions

- User A has access to all sections
- User B has limited permissions (some sections hidden in the previous sidebar)

## Test Data

| User | Expected Explore rows |
|------|-----------------------|
| User A | Agents, Pipelines, Skills, Toolkits & Indexes, MCPs, Applications, Credentials |
| User B | Only the sections visible to User B before the change, in the same relative order |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User A and open **Explore** | The rows match User A's Test Data row |
| 2 | Log in as User B and open **Explore** | The rows match User B's Test Data row |
| 3 | As User B, open the URL of a hidden section directly | Access behaves as it did before the change |

## Expected Final State

Each user sees only the sections they may access.

## Pass/Fail Criteria

**Pass:**
- Explore rows match the Test Data for both users

**Fail:**
- A section is shown to a user without access, or hidden from a user with access

## Notes

**Source functional tests:** ELITEA-5015
**Regression rationale:** Explore is now the only entry to every section; a wrong rule either hides features or exposes them.
**Selected checkpoints:** Full-access user; limited user; direct URL to a hidden section.
