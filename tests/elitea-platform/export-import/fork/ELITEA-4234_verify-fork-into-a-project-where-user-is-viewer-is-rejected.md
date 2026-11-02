---
id: ELITEA-4234
title: "Verify fork into a project where user is Viewer is rejected with \"Access denied\" and nothing is created"
priority: critical
type: functional
module: fork-import
status: draft
execution_type: manual
tags: [feat:settings, r-2.0.8, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#7057]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is Editor in Team Project A and Viewer in Team Project B (e.g. `Special Testing`)
- Team Project A contains an agent, a pipeline, a skill and a master agent with nested sub-agents and toolkits
- A second account with Editor or Admin rights in Team Project B is available
- DevTools Network tab is open

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Source project | Team Project A |
| Target project | Team Project B (user role: Viewer) |
| Expected error wording | contains "Access denied" |
| Expected response | HTTP 403, `access_denied` |

Entities (run all steps once per row):

| Entity | Where to start the fork |
|--------|-------------------------|
| Agent | Agents → agent details → ⋮ → VERSION → Fork |
| Pipeline | Pipelines → pipeline details → Fork |
| Skill | Skills → skill details → Fork |
| Agent with nested sub-agents and toolkits | Agents → master agent → Fork |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the user and open Team Project A | Project A is active |
| 2 | Open the entity from the Test Data row and start the Fork action | The Fork dialog opens with a target project selector |
| 3 | Open the target project selector and try to select Team Project B | Either Project B is not selectable, or it can be selected |
| 4 | If Project B was selected, click Fork | The fork is rejected; an error message containing "Access denied" is shown |
| 5 | Read the error message | It states the permission problem (not a generic failure); it contains no raw HTML or JSON |
| 6 | Check the dialog state | No success state and no "Got it" link are shown |
| 7 | In DevTools Network, inspect the fork request | Response status is 403 with body `access_denied` |
| 8 | Repeat steps 2–7 for every remaining row in the Test Data table | Results match steps 2–7 for every entity |
| 9 | Log in with the second account (Editor/Admin in Project B) and check Agents, Pipelines, Skills and Toolkits in Project B | No forked entity, sub-agent or toolkit from this test exists in Project B |

## Expected Final State

Forks of every entity type into Project B are blocked, the user sees a clear "Access denied" permission message, and Project B contains no new entities.

## Pass/Fail Criteria

**Pass:**
- Project B is not selectable, or the fork is rejected with an "Access denied" permission message
- The message has no raw HTML/JSON and no success state or "Got it" link is shown
- Response is 403 / `access_denied`
- Nothing is created in Project B

**Fail:**
- The fork succeeds or partially succeeds (any entity, sub-agent or toolkit created in Project B)
- The error is generic, lacks "Access denied", or shows raw HTML/JSON
- A success state or "Got it" link is shown
- The response is not 403 / `access_denied`
