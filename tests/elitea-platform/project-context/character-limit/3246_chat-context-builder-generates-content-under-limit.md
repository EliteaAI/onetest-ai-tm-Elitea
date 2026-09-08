---
id: "3246"
title: "Chat: Project Context Builder tool generates content ≤2500 characters"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, feat:chat, story:6344, r-2.0.6, project-context-builder, tool:generate_project_context_draft, character-limit]
requirements: [EliteaAI/elitea_issues#6344]
---

# 3246: Chat: Project Context Builder tool generates content ≤2500 characters

## Preconditions

- Chat with Project Context Builder module enabled
- User has Editor or Admin role
- Project exists with various assets (agents, pipelines, skills)

## Test Data

| Field | Value |
|-------|-------|
| Chat prompt | "Generate a project context for this project" |
| Character limit | 2500 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Chat in a project with multiple components | Chat loads successfully |
| 2 | Ensure Project Context Builder is enabled in settings | Module is active |
| 3 | Ask the AI to generate/create project context via chat | AI invokes generate_project_context_draft tool |
| 4 | Wait for generation to complete | AI produces project context |
| 5 | Verify the generated content length | Content is ≤2500 characters |
| 6 | Navigate to Settings → Project Context to verify | Generated content appears and respects limit |

## Expected Final State

Content generated via the Chat Project Context Builder tool does not exceed 2500 characters.

## Pass/Fail Criteria

**Pass:**
- Generated content ≤2500 characters
- Content is complete and coherent
- Content is saved to Project Context settings

**Fail:**
- Generated content exceeds 2500 characters
- Content is truncated or incomplete
- Save operation fails due to length
