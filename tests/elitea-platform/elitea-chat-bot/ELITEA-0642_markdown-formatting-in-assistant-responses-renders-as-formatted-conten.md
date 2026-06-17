---
id: ELITEA-0642
title: "Markdown formatting in assistant responses renders as formatted content, not raw syntax"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [markdown-rendering, response-rendering, rich-text, R-2.0.3]
requirements: [EliteaAI/elitea_issues#4775]
---
# ELITEA-0642: Markdown formatting in assistant responses renders as formatted content, not raw syntax

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** LLM-based agents routinely produce markdown-formatted responses. If markdown is not rendered, users see raw syntax like **bold** or - item instead of formatted text, which significantly degrades readability.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- Support Assistant panel is open with an active agent that can produce formatted responses

## Test Data

- Message to send: "Show me an example response that includes bold text, an inline code snippet, and a bullet list"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "Show me an example response that includes bold text, an inline code snippet, and a bullet list" in the input field and send it. | Message is submitted. Loading indicator shows. |
| 2 | Wait for the assistant response to fully render. | Response text appears in the conversation. |
| 3 | Look for bold text in the response. | The text intended to be bold is displayed in bold font weight — not shown with asterisks like **bold**. |
| 4 | Look for inline code in the response. | The code snippet is displayed in a distinct monospace or code font style — not shown with backticks. |
| 5 | Look for a bullet list in the response. | List items appear as a visual bulleted or numbered list — not as raw "- item" or "1. item" text. |
| 6 | If the response includes a fenced code block, look for a copy button on it. | A copy icon or button is visible on the code block allowing the user to copy the code. |

## Expected Final State

A copy icon or button is visible on the code block allowing the user to copy the code.

## Pass/Fail Criteria

Pass:
- Bold text renders as visually bold
- Inline code renders in a code style without backtick markers
- Bullet list renders as a visual list without dash markers
- No raw markdown syntax characters visible to the user

Fail:
- Raw asterisks, backticks, or dashes are visible in the response text
- All text renders as undifferentiated plain text
- Layout breaks or overflows when a formatted response is received
