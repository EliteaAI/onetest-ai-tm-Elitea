---
id: ELITEA-4207
title: "Pre-existing Skills created under the old 5000-character cap remain fully functional under the new 50000-character limit"
priority: medium
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:agents, feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6744]
---

## Preconditions

- A Skill exists that was created before this change, with instructions well under the old 5000-character cap.

## Test Data

| Field | Value |
|-------|-------|
| Pre-existing Skill | One Skill with instructions well under 5000 characters |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pre-existing Skill in the editor | Opens normally; instructions display unchanged |
| 2 | Save the Skill without modifying its instructions | Save succeeds |
| 3 | Attach the Skill to an agent and invoke it via chat (direct attachment and `~skill-name`) | Executes exactly as it did before this change, with full instructions applied |

## Expected Final State

The pre-existing Skill's behavior (edit, save, attach, invoke) is completely unaffected by the limit change from 5000 to 50000 characters.

## Pass/Fail Criteria

**Pass:**
- All steps complete with no behavioral difference from pre-change behavior.

**Fail:**
- The Skill fails to open, save, or execute correctly, or its instructions are altered in any way.
