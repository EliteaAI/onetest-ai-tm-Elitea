---
id: ELITEA-3767
title: Fork - Verify Multiple Fork Operations Preserve Editor Notes Correctly
module: Agent Management
feature: Agent Fork
priority: high
status: draft
tags:
  - feat:agents
  - eng:fork
  - editor-notes
  - workflow
  - EL-6156
related_issue: https://github.com/EliteaAI/elitea_issues/issues/6156
---

## Test Case Summary

Verify that Editor Notes are correctly carried over through multiple sequential fork operations (A → B → C), with modifications at each step, and that original agent values remain unchanged.

## Preconditions

- User is logged into ELITEA platform at https://next.elitea.ai/app/
- User has access to Private project
- User has permission to create, modify, and fork agents

## Test Data

| Agent | Editor Notes Value |
|-------|-------------------|
| Agent A (original) | "Original notes" |
| Agent B (fork of A, then modified) | "Modified in B" |
| Agent C (fork of B) | "Modified in B" (inherited) |

## Test Steps

### Phase 1: Create Original Agent A

| Step | Action | Expected Result |
|------|--------|----------------|
| 1 | Navigate to Agents page | Page loads |
| 2 | Create new agent "QA Agent A - Original" | Agent created |
| 3 | In Editor Notes, enter "Original notes" | Text entered |
| 4 | Save agent A | Agent saved successfully |
| 5 | Verify Editor Notes displays "Original notes" | ✅ Value correct |
| 6 | Record agent A URL/ID | ID recorded (e.g., agent-a-id) |

### Phase 2: Fork A → Create Agent B

| Step | Action | Expected Result |
|------|--------|----------------|
| 7 | Click Fork on agent A | Fork modal opens |
| 8 | Verify EDITOR NOTES in modal shows "Original notes" | ✅ Preview correct |
| 9 | Click Fork button | Fork completes |
| 10 | Navigate to agent B (forked agent) | Agent B page loads |
| 11 | Verify agent B name indicates fork (e.g., "QA Agent A - Original (forked)") | Name correct |
| 12 | Verify Editor Notes in B shows "Original notes" | ✅ Value inherited from A |
| 13 | Record agent B URL/ID | ID recorded (e.g., agent-b-id) |

### Phase 3: Modify Agent B Editor Notes

| Step | Action | Expected Result |
|------|--------|----------------|
| 14 | In agent B, click into Editor Notes field | Field focused |
| 15 | Clear existing text | Field empty |
| 16 | Enter "Modified in B" | New text entered |
| 17 | Click Save | Agent B saved |
| 18 | Reload agent B page | Page reloads |
| 19 | Verify Editor Notes shows "Modified in B" | ✅ New value persisted |

### Phase 4: Fork B → Create Agent C

| Step | Action | Expected Result |
|------|--------|----------------|
| 20 | Click Fork on agent B | Fork modal opens |
| 21 | Verify EDITOR NOTES in modal shows "Modified in B" | ✅ Preview shows B's current value |
| 22 | Click Fork button | Fork completes |
| 23 | Navigate to agent C (forked from B) | Agent C page loads |
| 24 | Verify agent C name indicates fork of B | Name correct |
| 25 | Verify Editor Notes in C shows "Modified in B" | ✅ Value inherited from B |
| 26 | Record agent C URL/ID | ID recorded (e.g., agent-c-id) |

### Phase 5: Verify Original Agent A Unchanged

| Step | Action | Expected Result |
|------|--------|----------------|
| 27 | Navigate back to agent A using recorded ID | Agent A page loads |
| 28 | Verify agent A Editor Notes still shows "Original notes" | ✅ A unchanged by B's fork |
| 29 | Verify A not affected by B's modification | ✅ Value still "Original notes" |
| 30 | Verify A not affected by C's creation | ✅ Value still "Original notes" |

## Expected Results

- ✅ Agent A created with "Original notes"
- ✅ Agent B inherits "Original notes" from A
- ✅ Agent B successfully modified to "Modified in B"
- ✅ Agent C inherits "Modified in B" from B
- ✅ Agent A remains unchanged at "Original notes" throughout
- ✅ Each fork operation correctly carries over current Editor Notes value

## Actual Results

_(To be filled during test execution)_

**Agent IDs:**
- Agent A: ________________
- Agent B: ________________
- Agent C: ________________

## Pass/Fail Criteria

**PASS:** All fork operations carry over correct Editor Notes values, modifications persist, and original agent unchanged

**FAIL:** Any of the following:
- Fork operation fails to carry over Editor Notes
- Editor Notes value incorrect at any step
- Modification to B fails to persist
- Agent A value changes unexpectedly
- Fork chain breaks at any point

## Notes

- Tests multi-step fork workflow
- Verifies fork operations are independent and don't affect source agents
- Verifies Editor Notes modifications persist and are carried forward
- Keep all three agents for traceability and debugging

