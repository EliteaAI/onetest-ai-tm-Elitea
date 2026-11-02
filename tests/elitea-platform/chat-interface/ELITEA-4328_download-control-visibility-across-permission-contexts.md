---
id: ELITEA-4328
title: "Download Control Visibility Across Project/Permission Contexts"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- Two users are available: a Private project owner, and a Team/shared project with both an owner and a non-owner participant
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment

## Test Data

| Context | User role |
|---|---|
| Private project | Project owner |
| Team project | Project owner |
| Team project | Non-owner participant |
| Prompt (all contexts) | "Give me a short json config example" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | As the Private project owner, navigate to `{{base_url}}/app/chat`, open/create a conversation, and send the Test Data prompt | AI responds with a code block showing the Download icon in its toolbar |
| 2 | Click Download as the Private project owner | File downloads successfully |
| 3 | As the Team project owner, open/create a shared conversation and send the same prompt | AI responds with a code block showing the Download icon in its toolbar |
| 4 | Click Download as the Team project owner | File downloads successfully |
| 5 | As a non-owner participant in the same Team project conversation, locate the same AI response's code block | Download icon is visible to the non-owner participant as well (download is a read-only, non-destructive action expected to be available to all participants who can view the message) |
| 6 | Click Download as the non-owner participant | File downloads successfully, with content matching the code block, consistent with the owner's experience |

## Expected Final State

The Download control is consistently visible and functional for a Private project owner, a Team project owner, and a Team project non-owner participant, with no unexpected permission-based restriction or exposure.

## Pass/Fail Criteria

**Pass:**
- Download icon and functionality are available and consistent across Private owner, Team owner, and Team non-owner participant contexts
- No role-based discrepancy causes the Download icon to be missing or non-functional where the user can otherwise view the message

**Fail:**
- Download icon is unexpectedly hidden, disabled, or errors for any of the tested roles/contexts
- A permission mismatch allows or blocks Download inconsistently with the platform's existing message-visibility rules
