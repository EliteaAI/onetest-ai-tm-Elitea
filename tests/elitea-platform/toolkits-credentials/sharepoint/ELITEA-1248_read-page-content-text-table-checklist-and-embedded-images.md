---
id: ELITEA-1248
title: "Read page content: text, table, checklist, and embedded images"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1248: Read page content: text, table, checklist, and embedded images

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that onenote_read_page and onenote_get_page_content correctly return page content including text, tables, checklists, and embedded images, with capture_images, include_attachments, and read_attachment_content flags behaving as documented.

**Coverage:**
- `onenote_get_page_content` returns raw XHTML with all elements visible
- `onenote_read_page` with `capture_images=False` replaces images with placeholder
- `onenote_read_page` with `capture_images=True` describes images via AI vision
- `include_attachments=True` appends an Attachments section
- `read_attachment_content=True` inlines parsed attachment text

## Preconditions

- A OneNote page exists containing: plain text paragraphs, a table (min 2×2), a checklist/to-do item, and at least one embedded image
- Agent with SharePoint toolkit (Delegated OAuth), LLM model configured

## Test Data

- Page ID: [page with text, table, checklist, embedded image]

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Invoke `Onenote get page content` with the target page ID. | Raw OneNote XHTML returned — structure of text, table, and checklist elements visible in the markup. |
| 2 | Invoke `Onenote read page` with capture_images=False, include_attachments=False. | Plain text content returned. Text paragraphs, table data, and checklist items all present and readable. Embedded images replaced with [image: <alt>] placeholder. |
| 3 | Invoke `Onenote read page` with capture_images=True, include_attachments=False. | Full content returned with embedded images described via AI vision — not a placeholder. All other elements still present. |
| 4 | Invoke `Onenote read page` with capture_images=False, include_attachments=True. | An "Attachments" section is appended listing filenames and download URLs. |
| 5 | Invoke `Onenote read page` with capture_images=True, include_attachments=True, read_attachment_content=True. | Full content returned: text, AI image descriptions, and inline parsed text from each attachment. |

## Expected Final State

Full content returned: text, AI image descriptions, and inline parsed text from each attachment.

## Pass/Fail Criteria

**Pass:**
- All content elements present across parameter combinations
- capture_images / include_attachments / read_attachment_content flags behave as documented

**Fail:**
- Any element silently missing; flags have no effect; tool errors on valid page ID
