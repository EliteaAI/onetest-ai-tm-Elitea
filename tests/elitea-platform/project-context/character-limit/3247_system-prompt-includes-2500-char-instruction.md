---
id: "3247"
title: "System prompt includes explicit 2500-character limit instruction"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, story:6344, r-2.0.6, project-context-builder, system-prompt, configuration]
requirements: [EliteaAI/elitea_issues#6344]
---

# 3247: System prompt includes explicit 2500-character limit instruction

## Preconditions

- Access to system prompt configuration or logs
- Ability to inspect the prompt sent to LLM for Project Context generation

## Test Data

| Field | Value |
|-------|-------|
| Expected instruction | "Keep output under 2500 characters" or equivalent |
| Generation endpoint | generate_project_context_draft |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Trigger Project Context generation (Settings or Chat) | Generation request is sent |
| 2 | Inspect the system prompt sent to the LLM (via logs, debug mode, or code review) | System prompt is visible |
| 3 | Search for character limit instruction in the prompt | Instruction to keep output ≤2500 chars is present |
| 4 | Verify the instruction is clear and explicit | No ambiguity in the limit requirement |

## Expected Final State

The system prompt for Project Context generation includes an explicit instruction to produce output under 2500 characters.

## Pass/Fail Criteria

**Pass:**
- System prompt contains explicit instruction about 2500-char limit
- Instruction is positioned prominently (not buried or easily ignored)
- Limit value matches the documented 2500 characters

**Fail:**
- No character limit instruction in system prompt
- Instruction uses different/wrong limit value
- Instruction is ambiguous or unclear
