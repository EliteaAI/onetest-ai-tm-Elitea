---
id: ELITEA-0580
title: "Support Assistant — Attaching Supported File and Sending Message Produces Valid Bot Response Without Socket Error"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0580: Support Assistant — Attaching Supported File and Sending Message Produces Valid Bot Response Without Socket Error

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that attaching each supported file type in the Support Assistant composer and sending a message produces a valid bot response without socket errors and the exchange is persisted in history. Re-validates the fix for bug EliteaAI/elitea_issues#4923.

**Coverage:**
- File attachment handling for all major supported types (.md, .txt, .docx, .pdf, .png, .jpg, .webp, .csv, .json, .xlsx)
- No socket error produced for any file type (regression of bug EliteaAI/elitea_issues#4923)
- Bot returns a meaningful response
- Sent message with attachment is visible in conversation history

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- 10 test files prepared on local machine (each < 5 MB)

## Test Data

| # | File | Type |
|---|---|---|
| 1 | README.md | Markdown |
| 2 | sample.txt | Plain text |
| 3 | sample.docx | Word document |
| 4 | sample.pdf | PDF |
| 5 | image.png | PNG image |
| 6 | photo.jpg | JPEG image |
| 7 | pic.webp | WebP image |
| 8 | data.csv | CSV |
| 9 | data.json | JSON |
| 10 | sample.xlsx | Excel (modern) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget by clicking the floating launcher | Widget opens with an empty composer |
| 2 | Start a new conversation. Click the paperclip icon | OS file browser opens |
| 3 | Select the test file for this iteration (repeat steps 3–7 for each file type from the table, one file per send) | File browser closes; file thumbnail/filename appears in the compose area |
| 4 | Type "Please summarize the content of the attached file." in the text input | Text appears. Send button becomes active |
| 5 | Click Send (or press Enter) | Message is submitted. No socket error. A loading indicator appears. |
| 6 | Wait for the bot response (up to 60 seconds) | Bot returns a meaningful, non-empty response. The sent message including the attachment name is visible in the thread. |
| 7 | Repeat steps 2–6 for each remaining file type in the table | All 10 file types produce a valid bot response |
| 8 | Open the conversation history in the Support Assistant | All conversations are listed with their messages saved |

## Expected Final State

All conversations are listed with their messages saved

## Pass/Fail Criteria

**Pass:**
- Each file type attaches without error
- No socket error for any file type (especially .md, .txt, .docx — regression EliteaAI/elitea_issues#4923)
- Bot responds with a meaningful reply for each type
- All messages with attachments are saved in history

**Fail:**
- Socket error occurs for any file type
- Bot returns no response (hangs or blank) for any file type
- Sent message is not saved in history
- Widget crashes or shows a blank state after attaching any file type
