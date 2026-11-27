---
id: ELITEA-5009
title: "Fork reflects the published version of the pipeline tree, not later changes in the source project"
priority: medium
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5009: Fork reflects the published version of the pipeline tree, not later changes in the source project

**Module:** agents-publishing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the fork brings the pipeline tree as it was when the version was published, that a new published version brings its own tree, and that each published version keeps its own pipelines.

---

## Preconditions

- The #7062 fix is deployed.
- In P-Author: agent **A** → pipeline **P1** (toolkit T1, agent node calling **A1** with toolkit T2, node calling pipeline **P2**). Published as version `v1`.
- Forker has 3 target projects: **P-Fork-1**, **P-Fork-2**, **P-Fork-3**.
- Optional: an agent **Old** with an attached pipeline that was published **before** the deploy.

---

## Test Data

| Change after v1 | Value |
|-----------------|-------|
| P1 | add a new node `extra_step` |
| A1 | change a T2 setting |
| P1 | remove the link to P2 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, make the 3 changes in P-Author. Don't publish. | Saved in P-Author. |
| 2 | As Forker, fork `v1` into P-Fork-1. | P1 has **no** `extra_step` node, A1's T2 has the **old** setting, and P2 is present and linked. |
| 3 | As Author, publish the changed A as version `v2`. As Forker, fork `v2` into P-Fork-2. | P1 has `extra_step`, T2 has the new setting, and P2 is **not** created. |
| 4 | As Author, remove P1 from A and publish as `v3`. Fork `v3` into P-Fork-3. | No pipeline is created. A's own toolkits are still forked. |
| 5 | Fork `v1` again into a new project. | It still brings the `v1` tree. |
| 6 | Edit the forked P1 in P-Fork-1. | P-Fork-2, the Catalog agent and P-Author are unchanged. |
| 7 | Fork agent **Old** (published before the fix). Then republish it and fork again. | The first fork has no pipeline. After republishing, the fork includes it. |
| 8 | **[Cleanup]** Delete the forked entities. Unpublish all test versions. | Cleanup done. |

---

## Expected Final State

Each fork matches the published version it came from.

---

## Pass/Fail Criteria

**Pass:**
- Unpublished source changes are not in the fork.
- Each published version brings its own pipeline tree.
- Forks are independent of each other and of the source.

**Fail:**
- A fork shows unpublished changes, or a version brings another version's pipelines.
