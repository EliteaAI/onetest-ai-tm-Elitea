---
id: ELITEA-5014
title: "Fork Pipelines — Catalog pipeline data holds no secrets, is restored only by a Catalog fork, and follows the published version"
priority: critical
type: regression
module: agents-publishing
status: draft
execution_type: manual
tags: [automated:API:regression, feat:import-forking, feat:pipelines, nfr:security, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5014: Fork Pipelines — Catalog pipeline data holds no secrets, is restored only by a Catalog fork, and follows the published version

**Module:** agents-publishing · **Priority:** critical · **Type:** regression

**Objective:** Regression of the secret stripping in `meta.fork_pipelines`, of the rule that only a Catalog fork restores it, and of the rule that the fork follows the published version and the Catalog copy has no tools. Manual source: ELITEA-5007, ELITEA-5008, ELITEA-5009.

---

## Preconditions

- JWT of Author (P-Author), of a Viewer outside P-Author, and of a teammate in team project P-Team.
- Created through the API in P-Author: agent A → pipeline P1 (GitHub toolkit with `ghp_FAKE7062`, remote MCP with header `Authorization: Bearer FAKE7062`, webhook trigger with a secret, a node calling pipeline P2) → agent A1 (toolkit with `jira_FAKE7062`).

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, publish A as `v1`. As Viewer, GET the Catalog version details. | 200. `tools` is empty. `meta.fork_pipelines` has `attached` and `nodes`. |
| 2 | Search the response for `ghp_FAKE7062`, `jira_FAKE7062`, `Bearer FAKE7062` and Author's email. | None found. The MCP header is `***MASKED***`. |
| 3 | Search for `parent_entity_id`, `parent_project_id`, `"application_id"`, `"application_version_id"`, `schedules`, `webhook_secret`. | None found. |
| 4 | As Viewer, call the plain export (not fork) of the Catalog agent. | 200. No pipelines and no `fork_pipelines` key. |
| 5 | In P-Team, PUT a team agent version with the `fork_pipelines` data from step 1 in its meta. As the teammate, fork it. | No pipeline from the planted data is created. |
| 6 | In P-Author, add node `extra_step` to P1 and remove the link to P2. Don't publish. As Viewer, fork `v1`. | P1 has no `extra_step`. P2 is created. The forked entities' meta has no `fork_pipelines` key and P1's trigger has no webhook secret. |
| 7 | As Author, try to publish P1 on its own. | Refused: "Pipeline agents cannot be published". |
| 8 | **[Cleanup]** Delete the forked and test entities. Unpublish A. | Done. |

---

## Notes

**Source functional tests:** ELITEA-5007, ELITEA-5008, ELITEA-5009
**Regression rationale:** The pipeline tree is stored in the public project, so a secret leak there is visible to every user, and the fork must follow the published snapshot.
