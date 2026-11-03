---
id: ELITEA-4317
title: "Download Button on Chat Code Block Produces File Matching Block Content"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- User has access to a Private project

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt (html) | "Generate a simple html page for test" |
| Prompt (css) | "Give me a css stylesheet example" |
| Prompt (json) | "Give me a sample json config object" |
| Prompt (xml) | "Give me a sample xml document" |
| Prompt (txt/no-tag) | "Give me a plain text note with no markdown language tag" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat` and start/open a direct chat conversation | Chat page loads with message input available |
| 2 | Send the prompt from the Test Data table for the "html" row | AI responds with a message containing a fenced code block |
| 3 | Locate the toolbar directly above the code block | Toolbar shows "Edit code", "Copy code", and a new "Download" icon |
| 4 | Click the Download icon | A file download is initiated and saved to the local downloads folder |
| 5 | Open the downloaded file in a text editor | File content exactly matches the code block content shown in chat, with no truncation or alteration |
| 6 | Repeat steps 2-5 for each remaining row in the Test Data table (css, json, xml, txt/no-tag) | For every code block type, a Download icon is present, a file downloads, and its content exactly matches the displayed code block |

## Expected Final State

For every tested code block language (html, css, json, xml, txt/no-tag), a file has been downloaded whose content is byte-for-byte identical to the corresponding code block rendered in the chat message.

## Pass/Fail Criteria

**Pass:**
- Download icon is present in the code block toolbar for every tested language
- Clicking Download produces a file in the downloads folder for every tested language
- Downloaded file content exactly matches the displayed code block content in every case

**Fail:**
- Download icon is missing for any tested language
- Clicking Download does not produce a file, or produces an error
- Downloaded file content differs from the displayed code block (truncated, corrupted, or altered)
