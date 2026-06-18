---
id: ELITEA-1237
title: "SharePoint Toolkit in Deeply Nested Structure — Agent with Multiple Sub-Agent Layers"
priority: medium
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, deep-nesting, qachk:4617, sub-agent, r-2.0.2, nested, oauth, p2]
requirements: [EliteaAI/elitea_issues#4335, EliteaAI/elitea_issues#4617]
---
# ELITEA-1237: SharePoint Toolkit in Deeply Nested Structure — Agent with Multiple Sub-Agent Layers

**Module:** Sharepoint · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that SharePoint OAuth login works correctly in a deeply nested structure with multiple sub-agent layers (e.g., Parent Agent -> Sub-Agent Level 1 -> Sub-Agent Level 2 -> SharePoint toolkit). Login prompt should surface correctly, authentication should complete, and the tool call should execute through all layers without breaking the chain.

## Preconditions

Logged into {{base_url}} as a private project user
Three-level agent structure exists:
  - Level 3 Agent: Has SharePoint toolkit (Delegated auth) with no valid token
  - Level 2 Agent: Has Level 3 Agent as sub-agent/tool
  - Level 1 Agent (Parent): Has Level 2 Agent as sub-agent/tool
Browser pop-ups are not blocked

## Test Data

Level 3 Agent: "SharePoint Reader" (has SharePoint toolkit, "Get files list" tool enabled)
Level 2 Agent: "Document Fetcher" (has "SharePoint Reader" as sub-agent)
Level 1 Agent (Parent): "Content Orchestrator" (has "Document Fetcher" as sub-agent)
SharePoint site: Valid SharePoint site URL configured in toolkit credentials
Prompt: "Use Document Fetcher to get SharePoint files via SharePoint Reader"
Environment: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Verify agent structure: Parent -> Sub-Agent L1 -> Sub-Agent L2 with SharePoint toolkit | All three agents exist with correct sub-agent relationships, Level 3 has SharePoint toolkit in 'Not Connected' state |
| 2 | Navigate to Chat and select Parent Agent (Content Orchestrator) | Chat opens with Parent Agent selected |
| 3 | Send prompt: 'Use Document Fetcher to get SharePoint files via SharePoint Reader' | Parent Agent begins processing, invokes Level 2 sub-agent, which invokes Level 3 sub-agent |
| 4 | Observe Chat when Level 3 sub-agent attempts to use SharePoint toolkit | Login prompt appears inline in Chat (not lost in deeply nested context) |
| 5 | Click the Login button in Chat | Microsoft OAuth popup opens |
| 6 | Complete OAuth login with valid credentials | OAuth popup closes, returns to Chat |
| 7 | Observe full response chain in Chat | Level 3 SharePoint tool executes successfully, results propagate up: Level 3 -> Level 2 -> Level 1 (Parent) |
| 8 | Verify Chat displays final response with SharePoint file listing | Parent Agent displays complete response including SharePoint data from deeply nested sub-agent |
| 9 | Check for any sub-agent invocation errors or broken chains | No errors, full invocation chain is intact and visible in Chat logs/response |

## Expected Final State

No errors, full invocation chain is intact and visible in Chat logs/response

## Pass/Fail Criteria

PASS:
- Login prompt appears in Chat despite deeply nested sub-agent structure (3 levels)
- OAuth flow completes successfully
- SharePoint tool executes within deepest sub-agent (Level 3)
- Results propagate correctly: Level 3 -> Level 2 -> Level 1 (Parent)
- No sub-agent invocation errors or broken response chain

FAIL:
- Login prompt does not appear (lost in nested context)
- OAuth completes but invocation chain breaks at any level
- SharePoint tool fails despite successful authentication
- Results do not propagate back to Parent Agent
- Any sub-agent layer reports invocation error or timeout
