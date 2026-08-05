---
id: ELITEA-2590
title: "[EliteaAI/elitea_issues#5844] ADO Wiki: Non-Image Attachment in Image Markdown"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [issue:5844, r-2.0.5, feat:toolkits, int:ado-boards, eng:ai, eng:backend, caching]
requirements: [EliteaAI/elitea_issues#5844]
---

# ELITEA-2590: ADO Wiki — Non-Image Attachment in Image Markdown

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that PDF/non-image attachments rendered with image markdown (!name) are not processed as images.

## Preconditions

- ADO toolkit configured with `process_images: true`
- Wiki page contains mixed attachments:
  - One real image (JPEG, PNG, GIF, WebP)
  - One PDF or document attachment rendered with `![filename](url)` syntax
- LLM/tool logs visible

## Test Data

| Attachment | Type | Markdown | Expected |
|-----------|------|----------|----------|
| Image.jpg | Image | ![image](url) | Processed |
| Document.pdf | PDF | ![pdf](url) | Skipped |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Read wiki page with real image and PDF using image markdown. | Page retrieved. |
| 2 | Verify real image is processed via LLM. | Image description generated; LLM called. |
| 3 | Verify PDF is NOT processed via LLM. | PDF attachment left untouched; no LLM call for PDF. |
| 4 | Check returned content: image has description, PDF untouched. | Image described; PDF markdown left as-is. |
| 5 | Verify no error text injected into page content. | No error messages about PDF in output. |
| 6 | Verify file type detection works correctly. | Tool correctly identifies PDF despite image markdown. |
| 7 | Check logs: confirm LLM called only for image, not PDF. | One LLM call (image only). |

## Expected Final State

- Real image gets described
- PDF/non-image attachment left untouched
- No error messages or changed behavior
- Correct content output
- File type detection working

## Pass/Fail Criteria

**Pass:** Image described; PDF skipped; no errors; logs show 1 LLM call (image only).  
**Fail:** PDF processed as image; errors generated; incorrect content; wrong LLM call count.
