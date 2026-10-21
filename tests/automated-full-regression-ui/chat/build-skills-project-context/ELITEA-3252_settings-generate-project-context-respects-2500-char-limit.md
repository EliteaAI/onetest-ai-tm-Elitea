---
id: ELITEA-3252
title: "Settings: Generate Project Context produces content ≤2500 characters"
priority: critical
type: functional
module: settings
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_build_with_ai_short_prompt_under_limit
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/cea34d4ac9ebd459fe1dda2cc3b08f3a59d128a8
tags: [automated:UI:regression, feat:project-setup, project-context-builder, character-limit]
requirements: [EliteaAI/elitea_issues#6344]
---

# ELITEA-3252: Settings: Generate Project Context produces content ≤2500 characters

**Module:** settings · **Priority:** critical · **Type:** functional

**Objective:** Verify that AI-generated project context content does not exceed the 2500 character limit.

---

## Preconditions

- User is logged in with Editor or Admin role
- Project Context page is accessible at Settings → Project Context
- Project Context toggle is enabled

---

## Test Data

| Field | Value |
|-------|-------|
| Project | Any test project with existing data |
| Character limit | 2500 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Project Context page loads |
| 2 | Enable the Project Context toggle if not already enabled | Toggle is ON, Edit/Edit with AI buttons become active |
| 3 | Click "Edit with AI" or "Build with AI" button | AI generation dialog/mode opens |
| 4 | Provide a project description and trigger generation | AI begins generating project context |
| 5 | Wait for generation to complete | Generated content appears in the editor |
| 6 | Check the character count of the generated content | Character count is displayed and is ≤2500 |

---

## Expected Final State

AI-generated project context content does not exceed 2500 characters.

---

## Pass/Fail Criteria

**Pass:**
- Generated content character count ≤ 2500
- Content is complete and coherent (not truncated mid-sentence)
- Character counter displays accurate count

**Fail:**
- Generated content exceeds 2500 characters
- Content is silently truncated
- Content ends abruptly mid-sentence or mid-word
