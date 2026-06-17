---
id: ELITEA-0906
title: "Supported File Types Accepted Across All Categories [Parametrized]"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0906: Supported File Types Accepted Across All Categories [Parametrized]

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that every supported file type category is accepted by the pipeline chat attachment system and the AI processes each file.

**Coverage:**
- Images: .png, .jpg, .gif, .webp
- Documents: .pdf, .docx, .pptx, .xlsx, .txt, .md
- Data: .csv, .json, .yaml, .xml
- Code: .py, .js, .ts, .java, .sql

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

| Category | Files |
|---|---|
| Images | img.png, img.jpg, img.gif, img.webp |
| Documents | doc.pdf, doc.docx, doc.pptx, doc.xlsx, doc.txt, doc.md |
| Data | data.csv, data.json, data.yaml, data.xml |
| Code | script.py, script.js, script.ts, script.java, query.sql |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat with paperclip active. | Chat input is ready. |
| 2 | For each file in the table: click the paperclip, select the file, type a prompt ('Analyze this file.'), and click Send. | File is accepted without an error — no 'unsupported type' rejection. Thumbnail or filename appears in input. |
| 3 | Wait for pipeline run completion for each file. | Pipeline returns a response referencing the file content. |
| 4 | Verify each uploaded file appears in the attachments bucket. | All files stored correctly. |

## Expected Final State

All files stored correctly.

## Pass/Fail Criteria

**Pass:**
- All listed file types accepted with no rejection error
- Pipeline responds for each file type

**Fail:**
- Any listed file type triggers 'unsupported type' error
- Any file type causes a pipeline run error
