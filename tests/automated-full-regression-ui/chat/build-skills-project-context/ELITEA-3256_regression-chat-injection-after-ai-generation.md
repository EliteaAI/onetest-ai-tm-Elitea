---
id: ELITEA-3256
title: "Regression: Project Context injection into Chat works after AI generation"
priority: high
type: regression
module: chat
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:project-setup, feat:chat, project-context-builder, regression]
requirements: [EliteaAI/elitea_issues#6344]
automation_test_id:
automation_pr:
---

# ELITEA-3256: Regression: Project Context injection into Chat works after AI generation

**Module:** chat · **Priority:** high · **Type:** regression

**Objective:** Verify that AI-generated Project Context is correctly injected into Chat conversations after generation.

---

## Preconditions

- User is logged in with Editor or Admin role
- Project Context generated via AI (Build with AI)
- Project Context toggle is ON
- Chat is accessible

---

## Test Data

| Field | Value |
|-------|-------|
| Generated context | AI-generated project context (≤2500 chars) |
| Test prompt | "What is this project about?" |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate Project Context via "Build with AI" | Content generated successfully |
| 2 | Verify content saved and toggle ON | Context saved, toggle enabled |
| 3 | Open a new Chat conversation | Chat loads |
| 4 | Ask: "What is this project about?" | AI responds |
| 5 | Verify AI response reflects the generated project context | Response uses project context info |

---

## Expected Final State

AI-generated Project Context is correctly injected into Chat conversations after generation.

---

## Pass/Fail Criteria

**Pass:**
- Chat AI response references/uses the generated context
- Context injection works the same as manually created context
- No errors in chat

**Fail:**
- Chat AI ignores the generated context
- Error when context is applied
- Different behavior compared to manual context
