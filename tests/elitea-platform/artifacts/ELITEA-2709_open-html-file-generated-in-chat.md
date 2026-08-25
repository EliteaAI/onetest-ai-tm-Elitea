---
id: ELITEA-2709
title: "Open HTML file generated in chat with View/Edit button"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User is in a chat session with an agent
- Agent has Artifacts toolkit available/enabled

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Prompt | "create an assistant landing page file in html format with headings, text formatting, lists, tables, images, inline styles, CSS styles within the HTML file, and report/dashboard layouts" |
| Expected output | assistant-landing-page.html (or similar) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Start a chat session with an agent that has Artifacts toolkit | Chat interface is ready |
| 2 | Send the HTML generation prompt | Agent processes the request |
| 3 | Wait for agent to generate the HTML file | Agent responds with generated file |
| 4 | Observe the chat response with generated file artifact | File appears as a clickable artifact item |
| 5 | Locate "View/Edit file" button/tooltip on the file artifact | View/Edit action is visible |
| 6 | Click "View/Edit file" | Canvas opens with the file |
| 7 | Verify the file opens in Preview mode | Preview tab is selected by default |
| 8 | Verify HTML content renders correctly | Content displays as formatted HTML |

## Expected Final State

- HTML file is generated successfully by the agent
- File opens in Canvas in Preview mode by default
- HTML renders correctly in Preview mode
- Can switch to Raw mode if needed

## Pass/Fail Criteria

**Pass:**
- Agent generates HTML file successfully
- File appears in chat as clickable artifact with file name and icon
- View/Edit action is available
- Clicking View/Edit opens Canvas in Preview mode
- HTML renders correctly

**Fail:**
- Agent fails to generate HTML file
- File artifact does not appear in chat
- View/Edit action is missing or non-functional
- Canvas opens in Raw mode instead of Preview
- HTML content does not render properly
