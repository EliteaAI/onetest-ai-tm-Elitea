---
id: ELITEA-0407
title: "Dismissing Tool Dropdown After Toolkit Selection Inserts Toolkit-Only Mention `/ToolkitName`"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0407: Dismissing Tool Dropdown After Toolkit Selection Inserts Toolkit-Only Mention `/ToolkitName`

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify a user can skip the second tool dropdown and keep only the Toolkit-level mention, resulting in `/ToolkitName` formatted in bold blue.

**Coverage:**
- Skip tool selection via Escape or clicking away
- /ToolkitName mention inserted (no tool sub-path)
- Mention is bold + blue

## Preconditions

- Jira Integration toolkit in Participants

## Test Data

- Toolkit: Jira Integration
- Expected mention: /Jira Integration (or /Jira)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat conversation with Jira Integration in Participants. | Jira Integration shown in Participants. |
| 2 | Click chat input, type /, select Jira Integration. | Second (tool) dropdown appears. |
| 3 | Press Escape or click outside the dropdown to dismiss. | Second dropdown closes without selecting a tool. |
| 4 | Inspect the chat input. | Only the Toolkit-level mention /Jira Integration is inserted. |
| 5 | Inspect the visual style. | Mention is bold and blue; no tool sub-path appended. |

## Expected Final State

Mention is bold and blue; no tool sub-path appended.

## Pass/Fail Criteria

**Pass:**
- /ToolkitName mention inserted (no tool)
- Mention is highlighted in bold + blue

**Fail:**
- No mention inserted after toolkit selection + dismiss
- Mention includes a tool path despite no tool being selected
