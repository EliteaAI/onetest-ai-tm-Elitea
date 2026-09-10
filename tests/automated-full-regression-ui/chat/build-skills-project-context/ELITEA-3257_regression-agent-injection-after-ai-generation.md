---
id: ELITEA-3257
title: "Regression: Project Context injection into Agents works after AI generation"
priority: high
type: regression
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:project-setup, feat:agents, project-context-builder, regression]
requirements: [EliteaAI/elitea_issues#6344]
automation_test_id:
automation_pr:
---

# ELITEA-3257: Regression: Project Context injection into Agents works after AI generation

**Module:** agents · **Priority:** high · **Type:** regression

**Objective:** Verify that AI-generated Project Context is correctly injected into Agent conversations.

---

## Preconditions

- User is logged in with Editor or Admin role
- Project Context generated via AI (Build with AI)
- Project Context toggle is ON
- Agent exists without "Ignore Project Context" enabled

---

## Test Data

| Field | Value |
|-------|-------|
| Generated context | AI-generated project context (≤2500 chars) |
| Test agent | Any agent without "Ignore Project Context" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate Project Context via "Build with AI" | Content generated successfully |
| 2 | Verify content saved and toggle ON | Context saved |
| 3 | Open an Agent page (not Chat) | Agent page loads |
| 4 | Run the agent with a context-related query | Agent executes |
| 5 | Verify agent response reflects the generated project context | Response uses project context |

---

## Expected Final State

AI-generated Project Context is correctly injected into Agent conversations.

---

## Pass/Fail Criteria

**Pass:**
- Agent response references/uses the generated context
- Injection works same as manually created context
- No errors

**Fail:**
- Agent ignores the generated context
- Error during agent execution
- Different behavior compared to manual context
