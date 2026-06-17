---
id: ELITEA-0688
title: "[DOCX Indexing] use_llm=false falls back to OCR — no \"Transcript is not available\" placeholder"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4794]
---
# ELITEA-0688: [DOCX Indexing] use_llm=false falls back to OCR — no "Transcript is not available" placeholder

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when use_llm is false (or omitted) for .docx in the chunking config, embedded images with text are processed via Tesseract OCR — not replaced with the "Transcript is not available" placeholder.

**Coverage:**
- OCR fallback is invoked when use_llm: false
- "Transcript is not available" placeholder is NOT produced when use_llm: false
- Image sections containing text return OCR-extracted content

## Preconditions

- Logged in to {{base_url}} under Private project
- Artifact toolkit with a bucket containing a .docx file with at least one embedded image that contains visible text (e.g., a chart label, screenshot with text)

## Test Data

- Chunking config (use_llm false): { ".docx": { "max_tokens": 512, "mode": "paged", "use_llm": false } }
- Test .docx file: contains embedded image(s) with legible text content
- Index name: docx-ocr-fallback

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifact toolkit → Indexes tab. Create a new index named docx-ocr-fallback. | New index entry created. |
| 2 | In Chunking Config, enter: { ".docx": { "max_tokens": 512, "mode": "paged", "use_llm": false } } | Config is accepted. |
| 3 | Click Index and wait for completion. | Run completes. Total indexed count is greater than 0. |
| 4 | Switch to the run tab. Select Search Index. Query for image-section content (e.g., 'image' or a text term visible in the image). | Results are returned. |
| 5 | Inspect any chunks with **Image Transcript:** prefix. | Chunks contain OCR-extracted text or an OCR-based result. The text 'Transcript is not available' does NOT appear. |

## Expected Final State

Chunks contain OCR-extracted text or an OCR-based result. The text 'Transcript is not available' does NOT appear.

## Pass/Fail Criteria

**Pass:**
- Image sections contain OCR output or recognizable extracted text
- "Transcript is not available" is absent from all image chunks

**Fail:**
- Any image chunk contains "Transcript is not available"
- No image-related chunks are returned at all
