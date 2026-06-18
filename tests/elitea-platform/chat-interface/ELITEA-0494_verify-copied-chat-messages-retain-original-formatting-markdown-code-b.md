---
id: ELITEA-0494
title: "Verify copied chat messages retain original formatting (markdown, code blocks, lists)"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat]
requirements: []
---
# ELITEA-0494: Verify copied chat messages retain original formatting (markdown, code blocks, lists)

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** When copying messages from chat using the copy button, the copied content loses its formatting. Markdown elements like code blocks, bold/italic text, bullet lists, and headers are stripped or flattened to plain text, making the copied output significantly different from the displayed message.

## Preconditions

User is logged into Elitea platform
A conversation exists or can be created
A text editor (e.g., VS Code, Notepad++) is available to paste and inspect copied content
User has access to Chat functionality

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open or create a conversation. Send a message that will elicit an AI response containing markdown formatting (e.g., 'Explain Python list comprehension with code examples and a bulleted summary') | AI responds with a formatted message containing code blocks, bullet points, and possibly headers or bold text |
| 2 | Verify the AI response renders with visible formatting: code blocks with syntax highlighting, bullet points, bold/italic text | Message displays with proper markdown rendering — code blocks are highlighted, lists are indented, text formatting is visible |
| 3 | Click the 'Copy to clipboard' button on the AI response message | Message content is copied to clipboard. A visual confirmation (e.g., tooltip or icon change) indicates successful copy |
| 4 | Paste the copied content into a plain text editor (e.g., Notepad, terminal) | Pasted content retains markdown syntax: code blocks wrapped in triple backticks, bullet points with - or *, headers with #, bold with ** |
| 5 | Paste the copied content into a markdown-capable editor (e.g., VS Code with markdown preview, a markdown-enabled input field) | Pasted markdown renders correctly in the target editor, matching the original chat display |
| 6 | Send another message with inline code ('Use `print()` and `len()` functions') and copy the AI response | Inline code formatting (backticks) is preserved in the copied text |
| 7 | Copy a user-sent message (not AI response) that contains formatting and paste it | User message formatting is also preserved when copied |
| 8 | Copy a message containing a numbered list and paste into a text editor | Numbered list structure (1. 2. 3.) is preserved in the pasted content |

## Expected Final State

Numbered list structure (1. 2. 3.) is preserved in the pasted content

## Pass/Fail Criteria

PASS: Copied messages retain markdown syntax (backticks, bullets, headers, bold markers) and render correctly when pasted into markdown editors
FAIL: Any formatting is lost — code blocks become plain text, list structure is removed, or markdown syntax markers are stripped from copied content
