---
id: ELITEA-5004
title: "Fork of a pipeline tree carries remote MCP, OpenAPI, local MCP and indexed toolkits, and creates shared entities once"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, feat:toolkits, feat:mcp, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5004: Fork of a pipeline tree carries remote MCP, OpenAPI, local MCP and indexed toolkits, and creates shared entities once

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that every toolkit type inside the pipeline tree is carried with the same rules as in #6859 (masked headers, stripped secrets, no index schedule), that a toolkit or agent used in several places is created once, and that two pipelines attached to the same agent are both forked.

---

## Preconditions

- Users Author (P-Author) and Forker (P-Fork), as in ELITEA-5002.
- The #7062 fix is deployed. The agent is published after the deploy.
- In P-Author:
  - Agent **A** with native toolkit **T1**, and pipelines **P1** and **P4** attached.
  - **P1** has the **same** toolkit T1, a **remote MCP** (URL, sensitive header `Authorization`, ordinary header `X-Client-Name`, 2 tools selected), an agent node calling **A1**, and a node calling **P2**.
  - **A1** has an **OpenAPI** toolkit (spec, a secret header, 2 operations selected).
  - **P2** has a **local MCP** connected in Author's environment, and an agent node calling the **same** A1.
  - **P4** has a native toolkit with an **index** (vector store + index schedule).
- Forker has **not** added the corresponding local MCP yet.

---

## Test Data

| Item | Where |
|------|-------|
| T1 (shared) | A and P1 |
| A1 (shared) | P1 and P2 |
| Remote MCP | P1 |
| OpenAPI | A1 |
| Local MCP | P2 |
| Indexed toolkit | P4 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, publish A. As Forker, fork it into P-Fork. | The fork succeeds with no error. |
| 2 | Open the forked A → toolkits. | A has T1, P1 and P4. |
| 3 | Open P-Fork → Toolkits and search for T1. | **One** T1 is created. Both A and P1 link to it. |
| 4 | Open P-Fork → Agents and search for A1. | **One** A1 is created. The agent nodes in P1 and P2 both use it. |
| 5 | Open P1's remote MCP. | URL, `X-Client-Name` and the 2 selected tools match. `Authorization` is **masked** (`***MASKED***`). |
| 6 | Open A1's OpenAPI toolkit. | Spec and the 2 operations match. The secret header is removed or masked. |
| 7 | Open P2's local MCP. | Attached and shown as **offline** / not available. |
| 8 | Open P4's indexed toolkit. | It uses P-Fork's vector store. No index schedule and no index data are copied. |
| 9 | Enter Forker's own MCP header, OpenAPI secret and native credentials. Chat with A using a task for P1, then a task for P4. | P1's MCP tool and A1's OpenAPI operation are called. P4 calls its toolkit. The offline local MCP causes no error. |
| 10 | As Forker, add the corresponding local MCP. Chat with a task that reaches P2. | The local MCP shows **online** and P2 calls it. |
| 11 | **[Cleanup]** Delete the forked entities in P-Fork. Unpublish A. | Cleanup done. |

---

## Expected Final State

Every toolkit type is carried to the right entity with masking and stripping applied. Shared toolkits and agents exist once. Both attached pipelines are present.

---

## Pass/Fail Criteria

**Pass:**
- Remote MCP, OpenAPI, local MCP and indexed toolkits are carried with the #6859 rules.
- T1 and A1 are each created once and linked from every place that uses them.
- P1 and P4 are both forked and attached.

**Fail:**
- A toolkit is missing, on the wrong entity, or shows a secret or sensitive header in clear.
- An index schedule is carried.
- A shared toolkit or agent is duplicated or linked from only one place, or an attached pipeline is missing.
