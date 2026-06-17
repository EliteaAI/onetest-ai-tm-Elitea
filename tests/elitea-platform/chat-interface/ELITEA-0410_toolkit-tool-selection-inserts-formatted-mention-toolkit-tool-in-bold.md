---
id: ELITEA-0410
title: "Toolkit + Tool Selection Inserts Formatted Mention `/Toolkit/tool` in Bold Blue"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [user_story:2925, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#2925]
---
# ELITEA-0410: Toolkit + Tool Selection Inserts Formatted Mention `/Toolkit/tool` in Bold Blue

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a toolkit and then a tool inserts a correctly formatted mention (`/Artifacts/create_file`) with bold blue visual styling.

**Coverage:**
- Mention format: /ToolkitName/toolName
- Visual style: bold + blue font
- Input remains editable after mention insertion

## Preconditions

- Artifacts toolkit in Participants

## Test Data

- Toolkit: Artifacts, Tool: create_file
- Expected mention: /Artifacts/create_file

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open chat conversation with Artifacts in Participants. | Artifacts shown in Participants panel. |
| 2 | Click chat input, type /, then select Artifacts. | Second dropdown appears. |
| 3 | Select create_file from the second dropdown. | Mention is inserted into the chat input. |
| 4 | Inspect the inserted text format. | Text reads /Artifacts/create_file (or equivalent). |
| 5 | Inspect the visual style of the inserted mention. | Mention is displayed in bold with blue text color. |
| 6 | Type additional text after the mention. | Additional text appears normally after the highlighted mention. |

## Expected Final State

Additional text appears normally after the highlighted mention.

## Pass/Fail Criteria

**Pass:**
- Mention inserted with correct format /ToolkitName/toolName
- Mention is visually highlighted (bold + blue)
- Input remains editable

**Fail:**
- Mention is plain text (not highlighted)
- Wrong format inserted
- Chat input becomes non-editable
