---
id: ELITEA-2809
title: "generate_skill_draft produces a valid JSON draft for a supported model and a complete description"
priority: high
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, skills-builder, tool:generate_skill_draft]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2809: generate_skill_draft produces a valid JSON draft for a supported model and a complete description

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "user_description": "Test with model gpt-5.6-luna", "llm_settings": {"model_name": "gpt-5.6-luna"}}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call generate_skill_draft with a supported model_name and a complete user_description | A valid JSON draft is returned containing populated name, description, and instructions fields |

## Expected Final State

A complete Skill draft request with a supported model returns a well-formed, usable JSON draft.

## Pass/Fail Criteria

**Pass:**
- Valid JSON draft with all three fields (name, description, instructions) populated and relevant

**Fail:**
- Malformed JSON, missing fields, or an empty response is returned
