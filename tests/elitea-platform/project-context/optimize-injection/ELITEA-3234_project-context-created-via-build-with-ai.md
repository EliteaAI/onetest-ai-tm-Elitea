---
id: ELITEA-3234
title: "Project Context Created via Build with AI and Used in Chat"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [project-context, chat, r-2.0.6, eng:optimization, build-with-ai]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- No Project Context exists yet OR existing context will be replaced

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-context` |
| Context Description | `This project focuses on generating high-quality test cases from provided Acceptance Criteria. Output should help QA teams validate requirements thoroughly.` |
| Test Phrase | `QA-BUILD-AI-TEST: Context created via Build with AI` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Project Context page loads |
| 2 | Click "Build with AI" button | Dialog "Build with AI" opens |
| 3 | Paste the Context Description into the input field | Text entered |
| 4 | Click "Generate Draft" button | AI generates Project Context draft based on description |
| 5 | Review generated draft, add test phrase: "QA-BUILD-AI-TEST: Context created via Build with AI" to the end | Draft looks good, test phrase added |
| 6 | Click "Apply" or "Save" | Project Context saved, toggle enabled |
| 7 | Navigate to Chat page, start new chat | Chat created |
| 8 | Send message: "What is the QA-BUILD-AI-TEST phrase?" | Chat invokes `Project Context: read_project_context` tool (visible in UI), returns: "Context created via Build with AI" |
| 9 | Ask: "What is this project about?" | Chat uses Project Context info, responds with test case generation / QA validation |
| 10 | Verify Project Context revision hash visible in tool call output | Revision hash displayed (e.g., `7f41325f...`) |

## Expected Final State

Project Context successfully created via "Build with AI", saved, and automatically invoked in chat when relevant prompts are sent. Context contains generated content plus test phrase. Tool call visible in chat UI.

## Pass/Fail Criteria

**Pass:**
- "Build with AI" generates draft successfully
- Draft can be edited and saved
- Project Context toggle enabled after save
- Chat invokes `read_project_context` tool when relevant
- Chat responses contain Project Context information
- Tool call visible in UI with revision hash

**Fail:**
- "Build with AI" fails to generate draft
- Cannot save generated context
- Context not invoked in chat
- Chat responses don't use context
- Tool call not visible or no revision hash
