---
id: ELITEA-4206
title: "Skill instructions near the 50000-character limit load and execute correctly through the full agent/chat runtime path"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:agents, feat:context-management, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6744]
---

## Preconditions

- User is logged in to `{{base_url}}`.
- An agent exists that can have Skills attached, with chat access.

## Test Data

| Field | Value |
|-------|-------|
| Skill instructions | ~49000–50000 characters, 2–3 Skills |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a Skill with instructions at ~49000–50000 characters and save it | Skill is created and saved successfully |
| 2 | Attach the Skill to an agent, reference it directly in the agent's own instructions, and send a chat message expected to trigger it | Full Skill instructions are loaded via `load_skill` with no truncation or error |
| 3 | In a new chat turn, invoke the same Skill via `~skill-name` instead | Skill resolves correctly and its full instruction content is applied |
| 4 | Attach 2–3 such large Skills to one agent and invoke multiple of them in a single turn, staying within the configured per-turn invocation cap | All invoked Skills execute with no errors, no silent truncation, and correct reconciliation when their instructions overlap |

## Expected Final State

Skills at or near the 50000-character limit behave identically to short Skills throughout the full runtime path — creation, attachment, `load_skill` loading, and `~name` invocation all carry the complete instruction text.

## Pass/Fail Criteria

**Pass:**
- Full, untruncated instruction content is loaded and applied in every invocation path tested, with no errors.

**Fail:**
- Any invocation path truncates, errors on, or fails to load the full instructions of a near-limit Skill.
