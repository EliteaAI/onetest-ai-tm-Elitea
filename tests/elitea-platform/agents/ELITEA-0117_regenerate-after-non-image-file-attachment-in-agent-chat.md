---
id: ELITEA-0117
title: "Regenerate After Non-Image File Attachment in Agent Chat"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:attachments, feat:agents]
requirements: [ProjectAlita/projectalita.github.io#3591]
---
# ELITEA-0117: Regenerate After Non-Image File Attachment in Agent Chat

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Regenerate button works correctly after sending a non-image file attachment in the Agents section — triggering a new generation rather than silently returning the same response.

**Coverage:**
- Regenerate after non-image file attachment as the first message in agent chat (minimum 1 file)
- Regenerate after non-image file attachment as the first message in agent chat (maximum 10 files)
- Regenerate after non-image file attachment as a non-first message in agent chat (minimum 1 file)
- Regenerate after non-image file attachment as a non-first message in agent chat (maximum 10 files)
- Non-image files are indexed into a vector database ("attach" collection) and retrieved via semantic search
- Supported non-image formats: .pdf, .doc/.docx, .ppt/.pptx, .xls/.xlsx, .txt, .md/.markdown, .json, .yaml/.yml, .csv, .xml, code files (.py, .js, .java, .cpp, .html, .css, .sql, .sh, etc.)

## Preconditions

- User is logged in to {{base_url}} — Private project active
- An agent is configured with "Allow attachments" toggle enabled and an Artifact bucket assigned in the Configuration tab
- Test non-image files prepared: at least 10 files (PDF and TXT recommended), each < 150 MB, total batch < 150 MB

## Test Data

Parametrization table:
| # | Message Position   | File Quantity       |
|---|--------------------|---------------------|
| 1 | First message      | 1 file (minimum)    |
| 2 | First message      | 10 files (maximum)  |
| 3 | Non-first message  | 1 file (minimum)    |
| 4 | Non-first message  | 10 files (maximum)  |

File specs: each file < 150 MB; total per message < 150 MB
Supported formats: .pdf, .doc, .docx, .ppt, .pptx, .xls, .xlsx, .txt, .md, .markdown, .json, .yaml, .yml, .csv, .xml, .py, .js, .java, .cpp, .html, .css, .sql, .sh
Text prompt: "Summarize the content"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agents section from the sidebar and open the configured agent (Allow attachments enabled, Artifact bucket assigned). | Agent chat interface is open and ready to receive input. |
| 2 | Parametrize by message position: - FIRST MESSAGE (variants 1, 2): Ensure the agent chat has no prior messages — open a fresh agent session if needed. - NON-FIRST MESSAGE (variants 3, 4): Send a plain text message (e.g. "Hello") and wait for the agent response before continuing. | First message variants: chat is empty. Non-first message variants: at least one prior exchange exists in the chat. |
| 3 | Click the paperclip (📎) icon in the message input area to open the file picker. | File selection dialog opens. |
| 4 | Attach non-image files per the active variant: - Variants 1 & 3 (minimum): attach 1 non-image file - Variants 2 & 4 (maximum): attach 10 non-image files Supported formats: .pdf, .doc/.docx, .ppt/.pptx, .xls/.xlsx, .txt, .md, .json, .yaml/.yml, .csv, .xml, code files. Each file < 150 MB; total < 150 MB. | File(s) appear as attachment chips in the message input area. |
| 5 | Type the text prompt: "Summarize the content". | Text prompt is entered alongside the attachment(s). |
| 6 | Click Send and wait for the agent to return a full response. | Agent produces a response based on the content of the attached file(s). |
| 7 | Click the Regenerate (🔄) icon located near the last agent message. | A new generation cycle starts — a loading indicator appears on the last message. |
| 8 | Wait for the regeneration to complete. | A new or refreshed response is produced. Behavior is consistent across all 4 parameter combinations. |

## Expected Final State

A new or refreshed response is produced. Behavior is consistent across all 4 parameter combinations.

## Pass/Fail Criteria

**Pass:**
- Loading indicator appears immediately after clicking Regenerate
- A new or refreshed response is produced
- No error message is displayed
- Behavior is consistent across all 4 parametrization combinations

**Fail:**
- No generation activity occurs after clicking Regenerate
- The same static response is returned silently with no loading indicator
- An error message is displayed
- Regenerate button is unresponsive or disabled
