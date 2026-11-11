---
id: ELITEA-4655
title: "Web Search Default Modules row is present with tooltip, and the Chats default toggle correctly propagates to a new chat and triggers a real web search"
priority: high
type: functional
module: default-modules
status: draft
execution_type: manual
tags: [feat:settings, feat:modules, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6982]
---

# ELITEA-4655: Web Search Default Modules Row, Tooltip, and Chat Inheritance

## Preconditions

- Logged in to `{{base_url}}` with permission to modify project settings
- Web Search is available for the current project (platform enabled, project enabled, shared toolkit resolved)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/settings/project-general` |
| Chat prompt | "search me some todays sport news article" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Settings → General → Default Modules | Default Modules section loads |
| 2 | Locate the Web Search row | Row shows a descriptive paragraph/label text |
| 3 | Hover over or inspect the Web Search row's tooltip | Tooltip is present (presence-only check; exact wording not asserted) |
| 4 | Inspect the Web Search row's toggle controls | Two separate toggles exist: one for Chats, one for Agents |
| 5 | Toggle the Chats default switch to ON and save | Change persists (confirm via reload if needed) |
| 6 | Navigate to Chats and create a new chat conversation | New chat opens |
| 7 | Click the "+" control in the new chat and open the Modules dropdown/flyout | Modules list opens |
| 8 | Scroll to the bottom of the Modules list | Web Search entry is present and shown toggled ON |
| 9 | Type the test prompt and send it | Message sends |
| 10 | Wait for the response to complete | Response renders |
| 11 | Inspect the response for web-search tool usage | A web-search tool-use indicator/chip is shown, or the tool call is visible in the model's thinking/trace steps |

## Expected Final State

The Web Search row in Default Modules is correctly documented with a tooltip, exposes independent Chats/Agents toggles, and the Chats default toggle correctly causes a newly created chat to inherit Web Search ON and actually invoke the web search tool when prompted.

## Pass/Fail Criteria

**Pass:**
- Web Search row paragraph and tooltip are both present
- Chats and Agents toggles are independently present
- New chat inherits Web Search ON from the Chats default
- The LLM visibly uses the web search tool in response to the test prompt

**Fail:**
- The row's description or tooltip is missing
- Only one combined toggle exists instead of separate Chats/Agents toggles
- The new chat does not inherit the Chats default
- No web-search tool-use indicator or trace step appears despite the toggle being ON
