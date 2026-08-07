---
id: ELITEA-1879
title: "Remove a tag from agent — removal persists after reload"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id:
  - tests.ui.agents.test_agent_management.TestAgentActions.test_remove_tag_from_agent_persists_after_reload
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1292
---

# ELITEA-1879: Remove a tag from agent — removal persists after reload

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that removing a tag from an agent and saving causes the tag to be permanently removed, with remaining tags staying intact after a page reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with at least one saved tag exists.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent that has at least one saved tag | The agent detail page loads with the saved tag(s) visible |
| 2 | Click the X on one tag to remove it | The tag chip disappears from the field |
| 3 | Verify the tag chip disappears from the field | The removed tag is no longer shown in the Tags field |
| 4 | Click Save | Save completes successfully |
| 5 | Reload the page | The page reloads |
| 6 | Verify the removed tag is no longer present; any remaining tags are intact | Removed tag is absent; all other tags are still displayed |

---

## Expected Final State

After reload, the removed tag is absent from the Tags field and all remaining tags are intact.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The removed tag does not reappear after reload; remaining tags are preserved.

**Fail:**
- Any step produces an error or unexpected result.
- The removed tag reappears after reload, or remaining tags are lost.
