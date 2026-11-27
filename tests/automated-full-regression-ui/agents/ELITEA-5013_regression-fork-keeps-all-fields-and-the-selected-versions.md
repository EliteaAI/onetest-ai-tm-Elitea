---
id: ELITEA-5013
title: "Fork Pipelines — Fork keeps every field and the selected version of each sub-agent and pipeline"
priority: high
type: regression
module: agents-publishing
status: draft
execution_type: manual
tags: [automated:API:regression, feat:import-forking, feat:pipelines, feat:versioning, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062", "EliteaAI/elitea_issues#7788"]
---

# ELITEA-5013: Fork Pipelines — Fork keeps every field and the selected version of each sub-agent and pipeline

**Module:** agents-publishing · **Priority:** high · **Type:** regression

**Objective:** Regression that the fork keeps every filled-in field and the selected (non-base) version of a sub-agent, a pipeline and an agent inside the pipeline, and that the published version, the snapshot and the forked entities use the selected version. Manual source: ELITEA-5005, ELITEA-5006.

**Known issue:** #7788 (description of the pipeline tree and editor notes are lost on fork).

---

## Preconditions

- JWT of Author (P-Author) and Forker (P-Fork).
- Created through the API in P-Author, each with a **base** version and a version **v2** with different content (markers `X-BASE` / `X-V2` in instructions):
  - Sub-agent **B**, pipeline **P1** (v2 has a node `v2_step`), and agent **A1** called by P1 v2's agent node (linked to A1 v2).
  - Agent **A** links B v2 and P1 v2.
- Every field from ELITEA-5005 is filled in on A, B v2, P1 v2 and A1 v2: description, tags, editor notes, instructions, welcome message, conversation starters, variables, LLM settings, step limit `17`, internal tools.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, publish A. GET the Catalog versions of A and the embedded B. | 200. B's embedded copy has the `B-V2` content. |
| 2 | GET A's Catalog version `meta.fork_pipelines`. | P1's node has `v2_step` and the A1 node has `A1-V2`. No `-BASE` marker is found. |
| 3 | As Forker, call the fork export. | 200. B, P1 and A1 carry the v2 content. No `-BASE` marker in the payload. |
| 4 | Fork into P-Fork. GET A, B, P1, A1. | Each has the v2 content. P1 has `v2_step`. |
| 5 | Compare every field of A, B, P1 and A1 with the source values. | All fields match, including step limit `17`, tags and internal tools. Description and editor notes are checked against #7788. |
| 6 | As Author, update the base versions of B, P1 and A1. Fork the same published version again. | The new fork still has the v2 content. |
| 7 | **[Cleanup]** Delete the forked and source entities. Unpublish A. | Done. |

---

## Notes

**Source functional tests:** ELITEA-5005, ELITEA-5006
**Regression rationale:** A wrong version or a lost field is silent: the fork succeeds, but the user gets different behaviour from what was published.
