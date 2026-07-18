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

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page and select a Draft version | The Draft version is loaded in the editor |
| 2 | Click the "Publish" button (requires applications.publish permission) | A dialog appears prompting for a version name |
| 3 | Verify a dialog appears prompting for a version name | The publish dialog with version name input is visible |
| 4 | Enter a version name (e.g., "v1-release") and click Publish | The publish action is submitted |
| 5 | Verify the version status changes (e.g., "In Review" or "Published" depending on moderation) | The version status is updated accordingly |
| 6 | If approved: verify the version appears as Published in the version dropdown | The version shows a Published status in the dropdown |
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
