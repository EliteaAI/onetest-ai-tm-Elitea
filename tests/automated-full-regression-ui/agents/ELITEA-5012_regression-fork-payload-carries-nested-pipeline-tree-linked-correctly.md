---
id: ELITEA-5012
title: "Fork Pipelines — Fork payload carries the nested pipeline tree linked correctly"
priority: high
type: regression
module: agents-publishing
status: draft
execution_type: manual
tags: [automated:API:regression, feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5012: Fork Pipelines — Fork payload carries the nested pipeline tree linked correctly

**Module:** agents-publishing · **Priority:** high · **Type:** regression

**Objective:** Regression of the fork payload for a published agent with nested pipelines and agents. Manual source: ELITEA-5002, ELITEA-5003, ELITEA-5004.

---

## Preconditions

- JWT of Author (project P-Author) and of Forker (project P-Fork).
- Created through the API in P-Author: native toolkit T1, agent A1 with toolkit T2, pipeline P2 with toolkit T3, pipeline P1 with toolkit T1 + an agent node calling A1 + a node calling P2, and agent A with toolkit T1 and P1 attached.

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, publish A through the API. | 200. Note the published version id in the public project. |
| 2 | As Forker, call the fork export for the published version. | 200. `applications` has A, P1, A1 and P2. |
| 3 | Check `agent_type` of P1 and P2. | `pipeline` for both. A1 is not `pipeline`. |
| 4 | Follow the `application` links from A's version `tools`. | A links to P1 through `settings.import_uuid` / `import_version_uuid`. |
| 5 | Follow the links from P1's version `tools`. | P1 links to A1 and P2, and to T1. |
| 6 | Check A1's and P2's version `tools`. | A1 has only T2. P2 has only T3. |
| 7 | Count toolkits by `import_uuid`. | All `import_uuid` values are unique. T1 is listed **once** and linked from A and P1. |
| 8 | Check every `application` link's `settings.import_uuid`. | Each one matches an entry in `applications`. |
| 9 | Call the fork export again. | Same `import_uuid` values as in step 2. |
| 10 | Import the payload into P-Fork (fork). GET A, P1, A1, P2 in P-Fork. | 200. All exist. P1 and P2 are pipelines, and the links point to entities in P-Fork. |
| 11 | **[Cleanup]** Delete the forked and source entities. Unpublish A. | Done. |

---

## Notes

**Source functional tests:** ELITEA-5002, ELITEA-5003, ELITEA-5004
**Regression rationale:** The fork payload is the contract between publish and fork. A missing or wrong link breaks every nested fork.
