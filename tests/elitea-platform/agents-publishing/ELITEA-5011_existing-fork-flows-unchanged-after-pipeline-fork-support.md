---
id: ELITEA-5011
title: "Existing fork and publish flows are unchanged after pipeline fork support"
priority: medium
type: regression
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5011: Existing fork and publish flows are unchanged after pipeline fork support

**Module:** agents-publishing · **Priority:** Medium · **Type:** Regression

**Objective:** Verify that forking team agents, forking Catalog agents without pipelines, forking into several projects, name conflicts, skills and the block on publishing pipelines work as before.

---

## Preconditions

- The #7062 fix is deployed.
- In team project **P-Team**: agent **TA** with an attached pipeline **TP** (with a toolkit).
- In P-Author: agent **N** without any pipeline (toolkits + one sub-agent + one skill), and agent **A** with pipeline **P1**, both published.
- Target project **P-Fork-X** already has a pipeline named `P1`, an agent named like P1's nested agent, and a toolkit named like P1's toolkit.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Fork team agent TA (not from the Catalog) into another project. | TA, TP and TP's toolkit are copied as before. |
| 2 | Fork Catalog agent N. | Toolkits, the sub-agent and the skill are forked as in #6859. No pipeline appears. |
| 3 | Fork Catalog agent A into two different projects. Edit P1 in one of them. | Each project has its own copies. The other project is unchanged. |
| 4 | Fork A into the **same** project a second time. | Record the result (related to #6905). If it succeeds, the new copies are linked to each other, not to the first fork. |
| 5 | Fork A into P-Fork-X. | The fork succeeds. Record whether names are changed. The forked A links to the **new** P1, and P1 links to the new nested agent and toolkit, not to the existing ones. |
| 6 | Try to publish pipeline P1 on its own from P-Author. | Blocked with "Pipeline agents cannot be published". |
| 7 | **[Cleanup]** Delete the forked entities. Unpublish the test agents. | Cleanup done. |

---

## Pass/Fail Criteria

**Pass:**
- Team forks, forks without pipelines and skill forks work as before.
- Forks into different projects are independent, and name conflicts don't link to existing entities.
- Publishing a pipeline on its own stays blocked.

**Fail:**
- Any of the existing flows changes behaviour or links to the wrong entity.
