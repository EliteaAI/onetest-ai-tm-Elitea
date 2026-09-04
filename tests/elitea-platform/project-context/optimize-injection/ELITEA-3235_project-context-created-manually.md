---
id: ELITEA-3235
title: "Project Context Created Manually (Without Build with AI) and Used in Chat"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [project-context, chat, r-2.0.6, eng:optimization, manual-creation]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- No Project Context exists yet OR existing context will be replaced

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-context` |
| Manual Context | `This is EliteA QA Testing Project. Focus: validating AI agent behavior and test automation. QA-MANUAL-TEST: Context created manually without AI assistance.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Settings → Project Context | Project Context page loads |
| 2 | Click "Create" button (NOT "Build with AI") | Editor mode opens |
| 3 | Manually type/paste the Manual Context text | Text entered |
| 4 | Enable Project Context toggle | Toggle enabled |
| 5 | Click "Save" | Project Context saved |
| 6 | Navigate to Chat page, start new chat | Chat created |
| 7 | Send message: "What is the QA-MANUAL-TEST phrase?" | Chat invokes `Project Context: read_project_context` tool (visible in UI), returns: "Context created manually without AI assistance" |
| 8 | Ask: "What is the focus of this project?" | Chat uses Project Context info, responds with "validating AI agent behavior and test automation" |
| 9 | Verify Project Context revision hash visible in tool call output | Revision hash displayed |

## Expected Final State

Project Context successfully created manually (without "Build with AI"), saved, and automatically invoked in chat when relevant prompts are sent. Tool call visible in chat UI.

## Pass/Fail Criteria

**Pass:**
- Manual context can be created and saved without using "Build with AI"
- Project Context toggle can be enabled
- Chat invokes `read_project_context` tool when relevant
- Chat responses contain manually entered context information
- Tool call visible in UI with revision hash

**Fail:**
- Cannot create context manually
- Cannot save manual context
- Context not invoked in chat
- Chat responses don't use context
- Tool call not visible
