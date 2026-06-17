---
id: ELITEA-0126
title: "Agent — Edit Description in non-latest version"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, R-2.0.1, agents, bug]
requirements: [ProjectAlita/projectalita.github.io#3076]
---
# ELITEA-0126: Agent — Edit Description in non-latest version

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Ensure that after the fix, the Description field on a non-latest Agent version can be edited, saved, and the change is reflected in all versions of the Agent.

## Preconditions

- Logged in to the application.
- User has permissions to create, update, and version Agents.
- No concurrent editors on the same Agent/version.

## Test Data

- Agent page: {{base_url}}
- Version name: "v2-qa-desc-20260305"
- Description to set: "Updated description for v2 — QA verification 20260305"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Agent page (HelloAgent). | Agent detail page loads successfully. |
| 2 | Save the Agent as a new version v2-qa-desc-20260305 and open it. | Version v2-qa-desc-20260305 is created and opens correctly. |
| 3 | Edit the Description field to "Updated description for v2 — QA verification 20260305" and click Save. | UI shows a success message; Save button reflects saved state. |
| 4 | Reload or reopen the same non-latest version. | Edited Description persists in this version. |
| 5 | Open other versions (including latest/base version). | Description is updated across all versions of the Agent. |

## Expected Final State

Description is updated across all versions of the Agent.

## Pass/Fail Criteria

Pass: Description persists in the edited version and is reflected in all versions; UI shows success.

Fail: Description does not persist in the edited version or change is not propagated to other versions.
