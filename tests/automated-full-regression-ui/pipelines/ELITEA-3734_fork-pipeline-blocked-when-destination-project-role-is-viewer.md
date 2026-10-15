---
id: ELITEA-3734
title: "Fork pipeline is blocked when user has only Viewer role in the destination project"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, feat:roles-permissions, issue:7013, r-2.0.7]
requirements: []
---

# ELITEA-3734: Fork pipeline is blocked when user has only Viewer role in the destination project

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a user cannot fork a pipeline into a project where they have only the Viewer role. The fork must be rejected with a permission-denied message, and no pipeline (or nested dependency) may be created in the destination project. Regression for [elitea_issues#7013](https://github.com/EliteaAI/elitea_issues/issues/7013).

---

## Preconditions

- User A is a member of Project A (source) with Editor (or higher) role.
- User A is a member of Project B (destination) with the **Viewer** role only.
- Project A contains an existing pipeline, ideally one with a nested agent or toolkit dependency.
- An admin/editor account for Project B is available to verify the result.

---

## Test Data

| Field | Value |
|-------|-------|
| Source project | Project A (User A: Editor) |
| Destination project | Project B (User A: Viewer) |
| Pipeline | Any existing pipeline in Project A, e.g. `Fork-Viewer-Check-Pipeline` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User A | User is logged in successfully |
| 2 | Switch to Project A and open the existing pipeline | The pipeline detail page opens |
| 3 | Click the three-dot menu (⋮) → select "Fork" | The Fork wizard opens |
| 4 | Open the destination project selector | Project B is either not listed, or is listed but cannot be selected / is marked as not permitted |
| 5 | If Project B can be selected: select Project B and click "Fork" / "OK" | The fork is rejected and a clear permission-denied error message is shown. No success state or "Got it" navigation is offered |
| 6 | (Optional, API) Send the fork request directly for Project B as User A (e.g. via DevTools "Copy as fetch" of a valid fork request with the target project ID changed to Project B) | The API returns an authorization error (403) and no entity is created |
| 7 | Log in as the Project B admin/editor and check Pipelines, Agents and Toolkits in Project B | No forked pipeline exists, and no nested agents/toolkits from the source pipeline were partially created |
| 8 | As User A, fork the same pipeline into a project where User A has Editor role | The fork succeeds, which confirms only the Viewer destination is blocked (clean up the forked entities afterwards) |

---

## Expected Final State

No pipeline or dependency is created in Project B. User A sees a permission-denied message, or cannot pick Project B as a fork destination. Forking into projects where User A has Editor rights still works.

---

## Pass/Fail Criteria

**Pass:**
- The fork into Project B is blocked in the UI and/or rejected by the backend with a permission error.
- No pipeline and no nested dependency appears in Project B.
- Forking into an Editor-role project still works.

**Fail:**
- The pipeline (or any of its dependencies) is forked and created in Project B even though User A has only the Viewer role there.
- The fork fails silently with no error message.
- Forking into a project where the user has Editor rights is also blocked.
