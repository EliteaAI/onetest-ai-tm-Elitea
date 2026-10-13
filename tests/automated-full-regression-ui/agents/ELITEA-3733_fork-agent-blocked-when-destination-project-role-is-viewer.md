---
id: ELITEA-3733
title: "Fork agent is blocked when user has only Viewer role in the destination project"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents, feat:roles-permissions, issue:7013, r-2.0.7]
requirements: []
---

# ELITEA-3733: Fork agent is blocked when user has only Viewer role in the destination project

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that a user cannot fork an agent into a project where they have only the Viewer role. The fork must be rejected with a permission-denied message, and no agent may be created in the destination project. Regression for [elitea_issues#7013](https://github.com/EliteaAI/elitea_issues/issues/7013).

---

## Preconditions

- User A is a member of Project A (source) with Editor (or higher) role.
- User A is a member of Project B (destination) with the **Viewer** role only.
- Project A contains an existing agent with at least one version.
- An admin/editor account for Project B is available to verify the result.

---

## Test Data

| Field | Value |
|-------|-------|
| Source project | Project A (User A: Editor) |
| Destination project | Project B (User A: Viewer) |
| Agent | Any existing agent in Project A, e.g. `Fork-Viewer-Check-Agent` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as User A | User is logged in successfully |
| 2 | Switch to Project A and open the existing agent | The agent detail page opens |
| 3 | Click the three-dot menu (⋮) → select "Fork" | The Fork wizard opens |
| 4 | Open the destination project selector | Project B is either not listed, or is listed but cannot be selected / is marked as not permitted |
| 5 | If Project B can be selected: select Project B and click "Fork" / "OK" | The fork is rejected and a clear permission-denied error message is shown. No success state or "Got it" navigation is offered |
| 6 | (Optional, API) Send the fork request directly for Project B as User A (e.g. via DevTools "Copy as fetch" of a valid fork request with the target project ID changed to Project B) | The API returns an authorization error (403) and no entity is created |
| 7 | Log in as the Project B admin/editor and open Agents in Project B | No agent named after the source agent (or marked "Forked from" Project A) exists in Project B |
| 8 | As User A, fork the same agent into a project where User A has Editor role | The fork succeeds, which confirms only the Viewer destination is blocked (clean up the forked agent afterwards) |

---

## Expected Final State

No agent is created in Project B. User A sees a permission-denied message, or cannot pick Project B as a fork destination. Forking into projects where User A has Editor rights still works.

---

## Pass/Fail Criteria

**Pass:**
- The fork into Project B is blocked in the UI and/or rejected by the backend with a permission error.
- No agent appears in Project B.
- Forking into an Editor-role project still works.

**Fail:**
- The agent is forked and created in Project B even though User A has only the Viewer role there.
- The fork fails silently with no error message.
- Forking into a project where the user has Editor rights is also blocked.
