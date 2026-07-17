---
id: ELITEA-1887
title: "Agent cannot be added to its own toolkit picker (self-attachment blocked)"
priority: medium
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_agent_self_attachment_blocked.TestAgentSelfAttachmentBlocked.test_agent_self_attachment_blocked
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/601
---

# ELITEA-1887: Agent cannot be added to its own toolkit picker (self-attachment blocked)

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that an agent cannot be added as a toolkit to itself — the agent should not appear in its own toolkit picker search results.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing agent is available.

---

## Test Data

| Field | Value |
|-------|-------|
| Search term | The current agent's own name |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to an agent detail page | The agent detail page loads |
| 2 | Click "+ Toolkit" to open the toolkit picker | The toolkit picker dialog opens |
| 3 | Search for the current agent's own name in the search field | Search results are returned |
| 4 | Verify the agent itself does NOT appear in the toolkit picker list | The current agent is absent from the search results |

---

## Expected Final State

The current agent does not appear in its own toolkit picker, preventing self-attachment.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The current agent is not present in its own toolkit picker search results.

**Fail:**
- Any step produces an error or unexpected result.
- The current agent appears in its own toolkit picker and could be attached to itself.
