---
id: ELITEA-5002
title: "Fork of a published agent creates its attached pipeline in the target project as a sub-agent"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5002: Fork of a published agent creates its attached pipeline in the target project as a sub-agent

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an agent with one attached pipeline is published and then forked from the Catalog, the pipeline is created in the target project as a pipeline, attached to the forked agent as a sub-agent, with the same nodes, settings and toolkit as in the published version. No manual re-creation may be needed.

---

## Preconditions

- Two users: **Author** (editor in project **P-Author**) and **Forker** (editor in project **P-Fork**).
- Publishing to the Catalog is enabled for P-Author.
- The #7062 fix (elitea_core#738) is deployed. The agent is published **after** the deploy.
- In P-Author:
  - Native toolkit **T1** (e.g. GitHub) with only **part** of its tools selected.
  - Pipeline **P1** with at least 3 nodes (one LLM node, one toolkit node using T1, one end node), 1 variable `topic` with a value, LLM settings and a step limit set.
  - Agent **A** with P1 attached as a sub-agent. Instructions have a fallback for unavailable tools.
- Valid credentials for T1 are available to Forker.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | `A-7062-basic` |
| Pipeline | `P1-7062-basic` |
| Pipeline variable | `topic` = `release notes` |
| Toolkit | T1, 2 of its tools selected |
| Prompt for the forked agent | "Use the pipeline to list the latest 3 issues." |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, open A → Publish, enter a version name, run the validation and publish. | Publishing succeeds. No "Pipeline agents cannot be published" error. |
| 2 | As Forker, open A in the Catalog → **Fork** → select **P-Fork**. | The fork wizard lists A, P1 and T1. It warns that credentials must be provided manually. |
| 3 | Complete the fork. | The fork succeeds with no error. |
| 4 | Open P-Fork → **Pipelines**. | `P1-7062-basic` is listed as a pipeline. |
| 5 | Open the forked A → Toolkits. | P1 is attached as a sub-agent. T1 is **not** attached to A (it belongs to P1). |
| 6 | Open the forked P1 → YAML / flow editor. Compare with the published version. | Nodes, connections and node settings are the same. |
| 7 | Check P1's variables, LLM settings and step limit. | `topic` = `release notes`. LLM settings and step limit match. |
| 8 | Open P1's toolkits. | T1 is attached to P1 with the **same** settings and only the 2 selected tools. |
| 9 | Open P-Fork → Toolkits. | T1 is listed and Forker can edit it. |
| 10 | Set Forker's credentials on T1. Chat with the forked A using the test prompt. | A calls P1, P1 runs its T1 node, and the answer contains data from T1. |
| 11 | **[Cleanup]** Delete the forked A, P1 and T1 in P-Fork. Unpublish A. | Cleanup done. |

---

## Expected Final State

The forked agent works with its pipeline right after the fork, once credentials are set. Nothing was re-created by hand.

---

## Pass/Fail Criteria

**Pass:**
- P1 is created as a pipeline and attached to the forked agent as a sub-agent.
- P1's nodes, variables, settings and toolkit match the published version.
- The forked agent runs the pipeline end to end.

**Fail:**
- P1 is missing, is created as a plain agent, or isn't attached.
- Any node, variable, setting or toolkit is missing or different.
- The user has to re-create or re-attach anything by hand.
