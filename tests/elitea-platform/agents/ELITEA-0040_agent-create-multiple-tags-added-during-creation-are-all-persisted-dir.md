---
id: ELITEA-0040
title: "[Agent Create] Multiple Tags Added During Creation Are All Persisted — Direct + Chat Participant [Parametrized]"
priority: medium
type: functional
module: agents
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0040: [Agent Create] Multiple Tags Added During Creation Are All Persisted — Direct + Chat Participant [Parametrized]

**Module:** Agents · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that adding multiple tags (system-existing and system-new) during agent creation correctly persists all of them after save, across both creation entry points.

**Coverage:**
- Creating agent via the direct Agents page creation form
- Creating agent via Chat Participants flow
- System-existing tags (already used elsewhere in the system) are persisted
- System-new tags (never used anywhere in the system) are persisted
- All tags survive navigation away and page reload

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Permissions to create agents
- Identify a tag already in use by at least one other agent or pipeline in the system (system-existing tag)
- Prepare 2 tag values that have never been used anywhere in the system (system-new tags)
- Browser: Chrome latest

## Test Data

**Variant A — Direct creation:**
- Agent name: TagTestAgent_Create
- Agent description: Test agent to verify tag persistence on creation
- Tags: ExistingSystemTag (system-existing), BrandNewTag_Create1 (system-new), BrandNewTag_Create2 (system-new)

**Variant B — Chat Participant creation:**
- Agent name: TagTestAgent_ChatParticipant
- Agent description: Test agent created via Chat Participants to verify tag persistence
- Tags: ExistingSystemTag (system-existing), BrandNewTag_Chat1 (system-new), BrandNewTag_Chat2 (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | **[Variant A]** Navigate to Agents → click Create Agent. **[Variant B]** Navigate to Chat, open the Participants panel, and initiate Create Agent from the Chat Participants flow. | Agent creation form/modal opens. |
| 2 | Fill in the agent name and description as per the test data for the chosen variant. | Name and description fields are populated. |
| 3 | Add the system-existing tag (ExistingSystemTag) to the tag field. | Tag chip appears in the field (autocomplete may suggest it). |
| 4 | Add the first system-new tag (BrandNewTag_Create1 or BrandNewTag_Chat1). | Second tag chip appears; 2 chips visible. |
| 5 | Add the second system-new tag (BrandNewTag_Create2 or BrandNewTag_Chat2). | Third tag chip appears; 3 chips visible. |
| 6 | Click Save / Create. | Agent is created successfully with no error. |
| 7 | Navigate to the Agents list and open the newly created agent. | Agent detail view loads. |
| 8 | Inspect the tag field. | All 3 tags — system-existing and both system-new — are present. |

## Expected Final State

All 3 tags — system-existing and both system-new — are present.

## Pass/Fail Criteria

**Pass:**
- All 3 tags are visible in the tag field after creation and navigation back to the agent
- Both variant A and variant B produce the same correct result

**Fail:**
- Any tag is missing after opening the created agent
- Regression in either creation flow
