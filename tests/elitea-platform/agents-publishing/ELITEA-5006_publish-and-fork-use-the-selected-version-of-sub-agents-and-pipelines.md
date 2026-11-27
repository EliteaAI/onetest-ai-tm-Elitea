---
id: ELITEA-5006
title: "Publish and fork use the selected version of each sub-agent and pipeline, not the base version"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, feat:versioning, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5006: Publish and fork use the selected version of each sub-agent and pipeline, not the base version

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a non-base version is selected for a sub-agent, a pipeline, or an agent inside a pipeline, publishing uses that version, chat with the published agent uses it, and the fork creates it. The base version must not be used anywhere.

---

## Preconditions

- Users Author (P-Author) and Forker (P-Fork), as in ELITEA-5002.
- The #7062 fix is deployed. The agent is published after the deploy.
- In P-Author, each entity has a **base** version and a version **v2**, with clearly different content:
  - Sub-agent **B**: base answers `B-BASE`; v2 answers `B-V2` and has toolkit **T-B2** (base has **T-B1**).
  - Pipeline **P1**: base has 2 nodes and toolkit **T-P1**; v2 has 3 nodes (one named `v2_step`) and toolkit **T-P2**.
  - Agent **A1** (called by P1's agent node): base instructions `A1-BASE`, v2 instructions `A1-V2`, with different toolkits.
- Agent **A** links B **v2** and P1 **v2**. P1 v2's agent node links A1 **v2**.

---

## Test Data

| Entity | Selected version | Base marker | v2 marker |
|--------|------------------|-------------|-----------|
| B | v2 | `B-BASE`, T-B1 | `B-V2`, T-B2 |
| P1 | v2 | 2 nodes, T-P1 | `v2_step` node, T-P2 |
| A1 | v2 | `A1-BASE` | `A1-V2` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, open A → toolkits. Check the version shown for B and P1. Open P1 v2 → its agent node. | B and P1 show **v2**. The agent node uses A1 **v2**. |
| 2 | Publish A. | Published. |
| 3 | As Forker, chat with the published A using a task for B. | The answer comes from B **v2** (`B-V2`), not `B-BASE`. |
| 4 | Fork A into P-Fork. Check the wizard. | The wizard shows B's toolkit T-B2 and P1's toolkit T-P2. T-B1 and T-P1 are not listed. |
| 5 | Open the forked B. | Its content is v2 (`B-V2`) with T-B2. |
| 6 | Open the forked P1. | It has 3 nodes including `v2_step`, and T-P2. |
| 7 | Open the forked A1. | Its instructions are `A1-V2` with v2's toolkits. |
| 8 | Check the links in the forked A and P1. | They point to the forked v2 content. Record which version name the forked entities get (e.g. `base`). |
| 9 | As Author, change the **base** versions of B, P1 and A1, and republish A. Fork again into a new project. | The fork still has the v2 content. Changes to base don't appear. |
| 10 | As Author, switch A's link to B **base** and publish a new version. Fork it. | The new fork has B's base content (`B-BASE`, T-B1). |
| 11 | **[Cleanup]** Delete the forked entities. Unpublish all test versions. | Cleanup done. |

---

## Expected Final State

The published agent and every fork use exactly the versions that were selected on the links when the agent was published.

---

## Pass/Fail Criteria

**Pass:**
- Publishing, chat with the published agent, and the fork all use the selected version of B, P1 and A1.
- Changes to the base version don't leak into the published agent or the fork.
- Switching the selected version and republishing changes the fork accordingly.

**Fail:**
- The base version (or any other non-selected version) is published, used in chat, or created by the fork, for any entity.
