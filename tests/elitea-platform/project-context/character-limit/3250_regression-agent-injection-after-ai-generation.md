---
id: "3250"
title: "Regression: Project Context injection into Agents works after AI generation"
priority: high
type: regression
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, story:6344, r-2.0.6, project-context-builder, regression, agents]
requirements: [EliteaAI/elitea_issues#6344]
---

# 3250: Regression: Project Context injection into Agents works after AI generation

## Preconditions

- Project Context generated via AI (Build with AI)
- Project Context toggle is ON
- Agent exists without "Ignore Project Context" enabled

## Test Data

| Field | Value |
|-------|-------|
| Generated context | AI-generated project context (≤2500 chars) |
| Test agent | Any agent without "Ignore Project Context" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate Project Context via "Build with AI" | Content generated successfully |
| 2 | Verify content saved and toggle ON | Context saved |
| 3 | Open an Agent page (not Chat) | Agent page loads |
| 4 | Run the agent with a context-related query | Agent executes |
| 5 | Verify agent response reflects the generated project context | Response uses project context |

## Expected Final State

AI-generated Project Context is correctly injected into Agent conversations.

## Pass/Fail Criteria

**Pass:**
- Agent response references/uses the generated context
- Injection works same as manually created context
- No errors

**Fail:**
- Agent ignores the generated context
- Error during agent execution
- Different behavior compared to manual context
