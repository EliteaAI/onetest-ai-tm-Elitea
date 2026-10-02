---
id: ELITEA-3459
title: "Plain-text document indexing records embedding tokens via the openai.embeddings dialect, no LLM spend"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, indexing]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6570"]
---

# ELITEA-3459: Plain-text document indexing records embedding tokens via the openai.embeddings dialect, no LLM spend

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that indexing a plain-text document (no embedded images, or `use_llm=false`) records embedding tokens using dialect `openai.embeddings` (or equivalent) — not `'unparsed'` — and produces **no** LLM (image-description) spend, only embedding-call spend.

---

## Preconditions

- Logged in to {{base_url}}.
- Artifact or SharePoint toolkit configured with a bucket.
- A plain-text document (e.g. `.txt` or a DOCX/PDF with no embedded images) ready to upload.

---

## Test Data

| Field | Value |
|-------|-------|
| Document | Plain-text file or image-free DOCX/PDF |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Upload the plain-text document to the configured bucket. | File is available for indexing. |
| 2 | Trigger indexing (via chat-driven `index_data` or the Toolkits UI). | Indexing completes successfully. |
| 3 | Inspect the resulting `usage_event` row(s) for this indexing operation. | Row(s) show embedding token usage with `dialect`/model consistent with `openai.embeddings` (or the configured equivalent) — not `'unparsed'`. |
| 4 | Verify no additional LLM (chat-completion-style) usage row was produced for image description. | No image-description LLM row exists, since the document has no embedded images. |

---

## Expected Final State

Plain-text indexing produces only embedding-usage rows via a correctly identified dialect, with no LLM image-description spend.

---

## Pass/Fail Criteria

**Pass:**
- Embedding row(s) present with correct dialect, non-zero tokens.
- No image-description LLM row is produced.

**Fail:**
- Dialect shows `'unparsed'` for a known embedding call.
- An unexpected LLM image-description row appears for an image-free document.
