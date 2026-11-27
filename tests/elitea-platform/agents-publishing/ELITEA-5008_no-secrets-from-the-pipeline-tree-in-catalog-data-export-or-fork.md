---
id: ELITEA-5008
title: "No secrets from any toolkit in the pipeline tree appear in the Catalog data, a plain export or the fork"
priority: critical
type: security
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, nfr:security, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062"]
---

# ELITEA-5008: No secrets from any toolkit in the pipeline tree appear in the Catalog data, a plain export or the fork

**Module:** agents-publishing · **Priority:** Critical · **Type:** Security

**Objective:** Verify that the pipeline data saved on the published version holds no secrets, masked headers stay masked, index and pipeline schedules and webhook secrets are not carried, source ids are not exposed, and the data can't be restored by a plain export or planted on a team agent.

---

## Preconditions

- The tree from ELITEA-5004 is published by Author (A → P1 → A1, P1 → P2 → A1, A → P4), with known fake secret values in every toolkit (e.g. `ghp_FAKE7062`, `jira_FAKE7062`, `Bearer FAKE7062`, OpenAPI secret `oa_FAKE7062`).
- **P1** has a **webhook trigger** with a webhook secret, and a **schedule**.
- A user **Viewer** who is not a member of P-Author, with a Keycloak JWT.
- Forker (P-Fork) and a teammate of Author in a team project **P-Team**.

---

## Test Data

| Field | Value |
|-------|-------|
| Fake secrets | `ghp_FAKE7062`, `jira_FAKE7062`, `Bearer FAKE7062`, OpenAPI secret `oa_FAKE7062` |
| Author email | Author's login email |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Viewer, GET the Catalog version details of the published A. | `meta.fork_pipelines` is present with `attached` and `nodes`. |
| 2 | Search the whole response for every fake secret and Author's email. | None of them appears. |
| 3 | Check the remote MCP entry in `fork_pipelines`. | The sensitive header value is `***MASKED***`. The ordinary header is kept. |
| 4 | Search the response for `parent_entity_id`, `parent_project_id`, `application_id`, `application_version_id`, `schedules`, `webhook_secret`, `webhook_signing_secret`. | None of them appears. Nodes are referenced by opaque keys (e.g. `n1`). |
| 5 | As Forker, fork A into P-Fork. Open the forked P1 → trigger settings and schedules. | No webhook secret is carried and no schedule is created. |
| 6 | Open every forked toolkit in P-Fork. | No secret is pre-filled. Masked headers show `***MASKED***`. |
| 7 | GET the forked A, P1 and A1 versions. | Their meta has no `fork_pipelines` key. |
| 8 | As Forker, **Export** (not Fork) the Catalog agent A and open the file. | The file has no pipelines and no `fork_pipelines` key. |
| 9 | In P-Team, PUT a team agent version with a copy of the `fork_pipelines` data in its meta. As the teammate, fork that agent into another project. | No pipelines from the planted data are created. |
| 10 | **[Cleanup]** Delete the forked entities and the team test agent. Unpublish A. | Cleanup done. |

---

## Expected Final State

No secret, email, schedule, webhook secret or source id from the pipeline tree is exposed anywhere.

---

## Pass/Fail Criteria

**Pass:**
- The Catalog data, the plain export and the fork contain no secrets, and masked headers stay masked.
- No schedules, webhook secrets, lineage or source ids are carried.
- Planted `fork_pipelines` data on a team agent is ignored.

**Fail:**
- Any secret, unmasked header, email, schedule, webhook secret or source id is exposed.
- A plain export or a team fork restores pipelines from the saved data.
