---
id: ELITEA-1892
title: "Publish a Draft version — status changes and Unpublish becomes available"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_publish_unpublish_version.TestAgentPublishUnpublishVersion.test_publish_draft_version_then_unpublish_reverts_to_draft
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/615
---

# ELITEA-1892: Publish a Draft version — status changes and Unpublish becomes available

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that publishing a Draft version changes its status and makes the Unpublish button available, and that clicking Unpublish returns the version to Draft status.

---

## Preconditions

- User is logged in to the Elitea platform.
- User has applications.publish permission.
- An agent with at least one Draft version exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Version name | v1-release |
| Category | Any valid category (e.g., "Quality Assurance", "Development", etc.) |
| Agent content | Instructions must contain substantive text (not just boilerplate); at least one Tag must be set. These are required to pass AI publish validation. |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page and select a Draft version | The Draft version is loaded in the editor |
| 2 | Click the "Publish" button (requires applications.publish permission) | A 3-step publish wizard dialog opens showing "Preparation" step with a Stepper (Preparation / Validation / Publishing) |
| 3 | **Preparation Step**: Fill in the required fields: (a) Version name input (e.g., "v1-release"), (b) Category dropdown selection (required), (c) Check "I agree with the Publishing Terms" checkbox | All three fields are filled/checked. The "Continue" button becomes enabled |
| 4 | Click "Continue" | AI validation fires (`POST /api/v2/.../publish_validate/...`). The wizard advances to "Validation" step showing validation results (Critical/Warning/Suggestion issues) |
| 5 | **Validation Step**: Review validation results. If Critical issues are present, return to agent editing to fix them (e.g., add tags, improve instructions). If no Critical issues, verify "Publish" button is enabled | If Critical issues exist (e.g., "No tags defined", "Instructions are missing"), the "Publish" button remains **disabled** and returns `422 Unprocessable Entity`. Fix issues and retry. If only Warnings/Suggestions, "Publish" button is **enabled** (`200 OK`) |
| 6 | Click "Publish" button on the Validation step | Publish action fires (`POST /api/v2/.../publish/...`). The app navigates to a **new version** (clone of the Draft) with the name specified in step 3 (e.g., "v1-release"). The version dropdown now shows **both** the original "base" (still Draft) and the new "v1-release" (Published). Toast confirms "The agent has been published." |
| 7 | Verify the "Unpublish" button is available on the published version | The Unpublish button is visible and clickable |
| 8 | Click Unpublish — verify the version status returns to Draft | The version status reverts to Draft |

---

## Expected Final State

After unpublishing, the version status is Draft again. The full publish/unpublish cycle completes without errors.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Version status changes on publish and reverts to Draft on unpublish; Unpublish button is available on published versions.

**Fail:**
- Any step produces an error or unexpected result.
- Version status does not change on publish, Unpublish button is unavailable, or status does not revert to Draft after unpublishing.
