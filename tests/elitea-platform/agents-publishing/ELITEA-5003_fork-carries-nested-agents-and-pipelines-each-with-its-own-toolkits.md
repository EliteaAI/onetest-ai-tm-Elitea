---
id: ELITEA-5003
title: "Fork carries nested agents and pipelines at any depth, each linked to the right parent with its own toolkits"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5003: Fork carries nested agents and pipelines at any depth, each linked to the right parent with its own toolkits

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that every agent and pipeline inside the attached pipeline is created by the fork, linked to the right parent in the target project, and keeps its own toolkits, settings and link variables. Covers a pipeline calling an agent, a pipeline calling a pipeline, a chain 4 levels deep, and a pipeline attached to an embedded sub-agent.

---

## Preconditions

- Two users: **Author** (editor in project **P-Author**) and **Forker** (editor in project **P-Fork**).
- The #7062 fix (elitea_core#738) is deployed. The agent is published **after** the deploy.
- In P-Author, this tree (all toolkits are native, e.g. GitHub or Jira):

```
A ─┬─ P1 (pipeline, toolkit T1)
   │    ├─ agent node → A1 (agent, toolkit T2)      link variable team = Backend
   │    └─ node → P2 (pipeline, toolkit T3)
   │                 └─ agent node → A2 (agent, toolkit T4)
   └─ B (plain sub-agent, toolkit T5)
        └─ P3 (pipeline, toolkit T6)
```

- A1 has its own variable `team` = `QA`. On the link from P1 to A1, `team` is overridden to `Backend`.
- Valid credentials for T1–T6 are available to Forker.

---

## Test Data

| Entity | Type | Toolkit | Parent |
|--------|------|---------|--------|
| P1 | pipeline | T1 | A |
| A1 | agent | T2 | P1 |
| P2 | pipeline | T3 | P1 |
| A2 | agent | T4 | P2 |
| B | agent (embedded) | T5 | A |
| P3 | pipeline | T6 | B |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, publish A. | Published. B is embedded and not listed as a separate Catalog card. |
| 2 | As Forker, fork A into P-Fork. Check the wizard. | The wizard lists all 7 entities and T1–T6. The fork succeeds. |
| 3 | Open P-Fork → Pipelines and Agents. | P1, P2, P3 are pipelines. A1, A2, B are agents. |
| 4 | Follow the links from the forked A: A → P1 → A1, P1 → P2 → A2, A → B → P3. | Every link points to the **forked** entity in P-Fork, not to P-Author. |
| 5 | Open each forked entity → toolkits. | Each has only its own toolkit (P1: T1, A1: T2, P2: T3, A2: T4, B: T5, P3: T6). A has P1 and B, but not P3. |
| 6 | Compare the nodes of P1, P2 and P3 with the published version. | Nodes and settings match. |
| 7 | Check A1's variables and the P1 → A1 link variables. | `team` = `QA` on A1, `Backend` on the link. |
| 8 | Check each toolkit's settings and selected tools. | They match the published version. |
| 9 | Set credentials. Chat with A using a task that runs A → P1 → P2 → A2. | Each level calls its own toolkit, and the answer contains data from T4. |
| 10 | Chat using a task that needs B's pipeline. | A delegates to B, B runs P3, and P3 calls T6. |
| 11 | **[Cleanup]** Delete the forked entities in P-Fork. Unpublish A. | Cleanup done. |

---

## Expected Final State

The full tree exists in the target project, linked as in the published version, with every toolkit on its own entity.

---

## Pass/Fail Criteria

**Pass:**
- Every nested agent and pipeline is created with the right type and linked to the right parent.
- Each toolkit is on its own entity only, with the same settings and selected tools.
- Link variables are preserved, and the chains run end to end.

**Fail:**
- Any entity is missing, has the wrong type, or links to the source project.
- A toolkit is missing or on the wrong entity, or a link variable is lost.
