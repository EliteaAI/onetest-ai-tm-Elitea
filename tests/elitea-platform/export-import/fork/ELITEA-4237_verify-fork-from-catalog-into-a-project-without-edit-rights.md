---
id: ELITEA-4237
title: "Verify fork from Catalog into a project without edit rights shows \"Access denied\""
priority: high
type: functional
module: fork-import
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is Viewer in Team Project B and Editor in Team Project A
- Catalog contains at least one published agent or skill
- A second account with Editor or Admin rights in Team Project B is available

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Catalog entity | a published agent or skill |
| Target project without edit rights | Team Project B (Viewer) |
| Target project with edit rights | Team Project A (Editor) |
| Expected error wording | contains "Access denied" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Catalog and find a published agent or skill | The entity details are shown |
| 2 | Click Fork and select Team Project B as the target | Either Project B is not selectable, or it can be selected |
| 3 | If Project B was selected, confirm the fork | The fork is rejected with an error message containing "Access denied"; no success state is shown |
| 4 | Log in with the second account and check Project B | No forked entity exists in Project B |
| 5 | As the original user, open the same Catalog entity, click Fork and select Team Project A | Fork completes successfully with no error |
| 6 | Open the forked entity in Project A | The entity exists in Project A and shows "Forked from" |

## Expected Final State

Fork from Catalog into a Viewer-only project is blocked with "Access denied" and creates nothing; fork into a project with Editor rights succeeds.

## Pass/Fail Criteria

**Pass:**
- Project B is not selectable, or the fork into it is rejected with "Access denied"
- Nothing is created in Project B
- Fork into Project A succeeds

**Fail:**
- The fork into Project B succeeds or shows a generic / raw HTML/JSON error without "Access denied"
- The fork into Project A fails
