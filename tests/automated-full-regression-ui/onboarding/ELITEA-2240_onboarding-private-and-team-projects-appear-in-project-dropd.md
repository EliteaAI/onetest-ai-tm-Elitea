---
id: ELITEA-2240
title: "Onboarding — Private and team projects appear in project dropdown after approximately 5 minutes"
priority: medium
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2240: Onboarding — Private and team projects appear in project dropdown after approximately 5 minutes

**Module:** onboarding · **Priority:** medium · **Type:** functional

**Objective:** Verify that Onboarding — Private and team projects appear in project dropdown after approximately 5 minutes. Success is confirmed when verify the full sidebar navigation items are now visible: chats, agents, pipelines, skills, toolkits, mcps, credentials, applications, artifacts, settings, catalog.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to the application for the first time | User is authenticated and lands on the expected landing page. |
| 2 | Click the project dropdown and verify no project is listed initially with limited sidebar items | Control responds; expected next state is shown. |
| 3 | Wait approximately 5 minutes for project provisioning to complete | Wait completes; subsequent state is ready. |
| 4 | Click the project dropdown again | Control responds; expected next state is shown. |
| 5 | Verify the Private project is now fully loaded with a checkmark indicator | Condition holds as described. |
| 6 | Verify team projects (if applicable for the user's account) are now listed in the dropdown | Condition holds as described. |
| 7 | Verify the full sidebar navigation items are now visible: Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Catalog | Condition holds as described. |

---

## Expected Final State

Verify the full sidebar navigation items are now visible: Chats, Agents, Pipelines, Skills, Toolkits, MCPs, Credentials, Applications, Artifacts, Settings, Catalog.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Onboarding — Private and team projects appear in project dropdown after approximately 5 minutes.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
