---
id: ELITEA-1241
title: "List and read file attachments on OneNote pages"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1241: List and read file attachments on OneNote pages

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that onenote_list_attachments and onenote_read_attachment correctly handle file attachments, that embedded images are handled via onenote_read_page, and that edge cases (empty page, wrong filename) behave correctly.

**Coverage:**
- onenote_list_attachments returns only user-uploaded file attachments (not embedded images)
- onenote_read_attachment parses attachment content by exact filename
- Embedded images handled via onenote_read_page with capture_images=True
- capture_images=False on onenote_read_attachment returns placeholder for image attachments
- Empty page returns empty list cleanly
- Wrong/misspelled attachment_name returns clear error

## Preconditions

- A OneNote page exists with at least one file attachment (e.g. PDF or DOCX uploaded as data-attachment) and at least one embedded image
- A second OneNote page with no attachments
- Agent with SharePoint toolkit (Delegated OAuth), LLM configured

## Test Data

- Page ID (with attachments): [page with file attachment and embedded image]
- Known attachment filename: [exact filename as uploaded, case-sensitive, e.g. report.pdf]
- Page ID (no attachments): [any page with no file attachments]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Onenote list attachments` for the page with attachments. | File attachment(s) listed with name, resource_id, download_url. Embedded images are NOT listed here — they are handled via onenote_read_page. |
| 2 | Invoke `Onenote read attachment` using page_id and the exact attachment_name (case-sensitive) from step 1. | Parsed text content of the file attachment returned (e.g. PDF/DOCX text extracted). |
| 3 | Invoke `Onenote read page` with capture_images=True for the same page. | Embedded image is described via AI vision in the page content output. Not returned by onenote_list_attachments. |
| 4 | Invoke `Onenote read attachment` with capture_images=False for an image attachment. | Image attachment returns [image: …] placeholder instead of AI description. |
| 5 | Invoke `Onenote list attachments` for a page with no attachments. | Empty list returned — no error. |
| 6 | Invoke `Onenote read attachment` with an incorrect attachment_name (wrong case or typo). | A clear descriptive error is returned — attachment not found. |

## Expected Final State

A clear descriptive error is returned — attachment not found.

## Pass/Fail Criteria

**Pass:**
- File attachments listed and readable by exact filename; embedded images handled via onenote_read_page
- Empty page returns empty list; wrong name returns clear error

**Fail:**
- File attachments not listed when they exist; read_attachment errors for valid filename; wrong case causes silent failure
