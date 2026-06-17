---
id: ELITEA-0627
title: "Support bot chat: sending a message with a file attachment produces a valid bot response and saves message history"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [support-bot, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4923]
---
# ELITEA-0627: Support bot chat: sending a message with a file attachment produces a valid bot response and saves message history

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Objective: Verify that attaching a file of any supported type in the support bot chat and sending a message produces a valid bot response without socket errors, and the message and response are correctly saved and visible in the support bot project chat history (admin view).

Coverage:
- File attachment handling in support bot chat for all relevant file types
- Socket connection stability when files are attached
- Message and response persistence in support bot chat history (admin view)

Test data (repeat steps for each file type):

| # | File | Type |
| 1 | README.md | Markdown |
| 2 | sample.txt | Plain text |
| 3 | sample.docx | Word document |
| 4 | sample.pdf | PDF |
| 5 | sample.ppt | PowerPoint |
| 6 | sample.pptx | PowerPoint (modern) |
| 7 | sample.xls | Excel 97 |
| 8 | sample.xlsx | Excel (modern) |
| 9 | sample.html | HTML |
| 10 | sample.htm | HTM |
| 11 | sample.xml | XML |
| 12 | sample.yaml | YAML |
| 13 | sample.yml | YML |
| 14 | data.json | JSON |
| 15 | data.jsonl | JSONL |
| 16 | data.csv | CSV |
| 17 | sample.groovy | Groovy source |
| 18 | image.png | PNG |
| 19 | photo.jpg | JPG |
| 20 | photo2.jpeg | JPEG |
| 21 | pic.webp | WEBP |
| 22 | anim.gif | GIF |

## Preconditions

- Logged in to ELITEA
- Support bot chat widget is available in the sidebar
- Test files of each type are prepared locally (as per Test Data table in Description)
- Admin access available to verify support bot project chat history

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the support bot chat (sidebar widget). | Support bot chat opens and is ready to accept input. |
| 2 | Attach the file for this data variant (see Test Data table). | File is attached and shown in the chat input area. |
| 3 | Type any message (e.g. "Please review this file") and send it. | Message is sent; no socket error occurs. |
| 4 | Wait for the bot to respond. | Bot returns a valid response. No socket error is displayed to the user. |
| 5 | As admin, open the support bot project chat history and locate the conversation. | The sent message and bot response are visible and correctly saved in the chat history. |

## Expected Final State

The sent message and bot response are visible and correctly saved in the chat history.

## Pass/Fail Criteria

Pass:
- Bot responds successfully for every file type in the Test Data table
- No socket errors occur
- Message and response are saved and visible in admin chat history for all file types

Fail:
- Socket error occurs for any file type (bug EliteaAI/elitea_issues#4923 specifically triggers on .md, .txt, .docx and similar text/document types)
- Bot does not respond after sending a message with an attachment
- Message or response is missing from admin chat history after the send
