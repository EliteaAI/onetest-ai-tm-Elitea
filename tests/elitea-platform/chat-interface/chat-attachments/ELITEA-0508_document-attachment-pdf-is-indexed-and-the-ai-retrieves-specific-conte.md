---
id: ELITEA-0508
title: "Document attachment (.pdf) is indexed and the AI retrieves specific content via semantic search"
priority: critical
type: functional
module: chat-attachments
status: ready
execution_type: manual
tags: [feat:attachments, issue:1285, feat:chat, r-2.0.0b]
requirements: [ProjectAlita/projectalita.github.io#1285]
---
# ELITEA-0508: Document attachment (.pdf) is indexed and the AI retrieves specific content via semantic search

**Module:** Chat Attachments · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that attaching a PDF document causes it to be indexed into the vector database, and the AI can retrieve and answer questions about specific content within the document using semantic search — with the file stored automatically in the default `attachments` bucket.

**Coverage:**
- PDF file is accepted without error and thumbnail appears in input
- LLM responds with content drawn from the attached PDF
- Specific named content is retrievable via semantic query
- File stored in default `attachments` bucket automatically
- Non-image files are processed via indexing + semantic retrieval (not direct vision)

## Preconditions

- Logged into ELITEA at {{base_url}}
- Direct LLM chat or Agent with attachments enabled
- A `.pdf` file with known, unique content available locally

## Test Data

- File: `test_document.pdf` containing text "Section 3: Project Milestones include Q3 delivery of API module"
- Query 1: "What are the project milestones?"
- Query 2: "What is scheduled for Q3?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation → click the paperclip icon → select `test_document.pdf` | File thumbnail appears in the input area; no 'unsupported type' error |
| 2 | Type "What are the project milestones?" → click Send | AI responds with the milestones content from the PDF (including 'Q3 delivery of API module') |
| 3 | Send a follow-up: "What is scheduled for Q3?" | AI retrieves and returns the Q3 content from the indexed document — matching the PDF's unique phrase |
| 4 | Verify no errors and content is accurate | All responses match the PDF content; no generic 'I don't have information' response; no upload errors |
| 5 | Navigate to Artifacts → check the `attachments` bucket | `test_document.pdf` appears in the `attachments` bucket |

## Expected Final State

`test_document.pdf` appears in the `attachments` bucket

## Pass/Fail Criteria

**Pass:**
- PDF accepted without error
- AI returns content specific to the attached PDF for both queries
- File found in `attachments` bucket after sending
- No error messages

**Fail:**
- PDF rejected or upload error shown
- AI returns generic response not based on the PDF content
- File missing from `attachments` bucket
