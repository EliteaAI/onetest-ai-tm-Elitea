---
id: ELITEA-3253
title: "Settings: Generate Project Context shows error when output would exceed 2500 characters"
priority: critical
type: functional
module: settings
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.settings.test_project_context_ai_generation_char_limit.TestProjectContextAIGenerationCharLimit.test_build_with_ai_verbose_prompt_exceeds_limit
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/cea34d4ac9ebd459fe1dda2cc3b08f3a59d128a8
tags: [automated:UI:regression, feat:project-setup, project-context-builder, error-handling]
requirements: [EliteaAI/elitea_issues#6344]
---

# ELITEA-3253: Settings: Generate Project Context shows error when output would exceed 2500 characters

**Module:** settings · **Priority:** critical · **Type:** functional

**Objective:** Verify that when AI generation would produce content exceeding 2500 characters, an error message is displayed and no truncated content is saved.

---

## Preconditions

- User is logged in with Editor or Admin role
- Project Context page is accessible at Settings → Project Context
- Project Context toggle is enabled

---

## Test Data

| Field | Value |
|-------|-------|
| Complex prompt | "Create a comprehensive and detailed project context for a large-scale AI-powered Healthcare Appointment and Patient Management Platform. The project should include multiple user roles such as patients, doctors, nurses, clinic administrators, and system administrators. Describe the project's business goals, key features, user workflows, functional and non-functional requirements, system architecture, frontend and backend components, database structure, authentication and authorization, appointment scheduling, patient records, notifications, billing, reporting, audit logging, integrations with external healthcare systems and payment providers, API requirements, data validation, error handling, security and privacy considerations, performance requirements, scalability, accessibility, localization, and compliance requirements." |
| Character limit | 2500 |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Project Context page loads |
| 2 | Enable the Project Context toggle if not already enabled | Toggle is ON |
| 3 | Click "Edit with AI" button | AI generation dialog opens |
| 4 | Enter the complex prompt from Test Data that would generate verbose output | Prompt is entered in the input field |
| 5 | Click "Generate Draft" button | System attempts to generate content |
| 6 | Observe the result | Error message is displayed: "Project background is X characters, the maximum is 2500. Try generating again, or ask for a narrower scope." |
| 7 | Verify the original prompt remains in the input field | Prompt is preserved, user can edit it |
| 8 | Verify no partial/truncated content was saved | Project Context field is unchanged |

---

## Expected Final State

- Error message clearly indicates the generated content exceeded 2500 characters
- Original prompt remains in the input field for user to modify
- No partial or truncated content is generated or saved

---

## Pass/Fail Criteria

**Pass:**
- Clear error message displayed with character count (e.g., "Project background is 5893 characters, the maximum is 2500")
- Suggestion to "Try generating again, or ask for a narrower scope" is shown
- Original prompt preserved in input field
- No content generated or saved to Project Context

**Fail:**
- Content is silently truncated and saved
- No error message shown when limit exceeded
- Original prompt is lost/cleared
- Partial content is displayed or saved
