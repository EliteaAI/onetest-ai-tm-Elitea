---
id: ELITEA-5005
title: "Publish and fork keep every filled-in field of the agent, its sub-agents and its pipeline tree"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:import-forking, feat:pipelines, issue:7062, r-2.0.9]
requirements: ["EliteaAI/elitea_issues#7062", "EliteaAI/elitea_issues#7788"]
---

# ELITEA-5005: Publish and fork keep every filled-in field of the agent, its sub-agents and its pipeline tree

**Module:** agents-publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when every field is filled in on the agent, an embedded sub-agent, an attached pipeline and the agent called by that pipeline, the published version shows the right values and the fork keeps all of them. No field may be lost or changed.

**Known issue:** #7788. Description of the pipeline tree and editor notes are lost on fork. Until it is fixed, those rows are expected to fail.

---

## Preconditions

- Users Author (P-Author) and Forker (P-Fork), as in ELITEA-5002.
- The #7062 fix is deployed. The agent is published after the deploy.
- In P-Author: agent **A** → embedded sub-agent **B**, and A → pipeline **P1** → agent node → agent **A1**.
- Each of A, B, P1 and A1 has **every** field below filled in with a unique value (prefix with the entity name, e.g. `A-desc`, `P1-desc`).

---

## Test Data

| Field | Value on each entity (example for A) | Applies to |
|-------|--------------------------------------|------------|
| Name | `A-7062-fields` | all |
| Description | `A-desc: forks pipelines` (at least 30 characters) | all |
| Tags | `fork-7062`, `A-tag` | all |
| Editor notes | `A-notes: do not delete` | all |
| Instructions | `A-instr: You help with releases.` | agents |
| Welcome message | `A-welcome` | agents |
| Conversation starters | `A-start-1`, `A-start-2` | agents |
| Variables | `topic` = `A-topic` | all |
| Model and LLM settings | a specific model, temperature `0.3`, max tokens `2048` | all |
| Step limit | `17` (not the default) | all |
| Internal tools | at least 2 enabled (e.g. Planner, Attachments) | agents |
| Icon | a custom icon | all |
| Pipeline YAML / nodes | at least 3 nodes, one with non-default settings | P1 |
| Toolkit selected tools | a subset of tools | each toolkit |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As Author, record every field of A, B, P1 and A1 (screenshot or export). | Values recorded. |
| 2 | Publish A. | Published. |
| 3 | As Forker, open A in the Catalog → details. | A's name, description, tags, welcome message, conversation starters and icon are shown as recorded. |
| 4 | Start a chat with the published A. | The welcome message and conversation starters are A's. |
| 5 | Fork A into P-Fork. | The fork succeeds. |
| 6 | Open the forked **A** and compare every field with step 1. | All fields match: name, description, tags, editor notes, instructions, welcome message, conversation starters, variables, model and LLM settings, step limit `17`, internal tools, icon. |
| 7 | Do the same for the forked **B**. | All fields match B's values. |
| 8 | Do the same for the forked **P1**, including the pipeline nodes. | All fields match P1's values. Nodes and node settings are the same. |
| 9 | Do the same for the forked **A1**. | All fields match A1's values. |
| 10 | Check each forked toolkit's selected tools. | Only the recorded subset is selected. |
| 11 | Check that no field was mixed up between entities (e.g. A1 doesn't show `A-notes`). | Each entity has its own values. |
| 12 | **[Cleanup]** Delete the forked entities in P-Fork. Unpublish A. | Cleanup done. |

---

## Expected Final State

Every field of every forked entity matches the source values recorded before publishing.

---

## Pass/Fail Criteria

**Pass:**
- Every field in the Test Data table is kept on A, B, P1 and A1 after the fork.
- No value is moved to another entity.

**Fail:**
- Any field is empty, reset to the default, or different after the fork. List each failing field and entity in the result.
