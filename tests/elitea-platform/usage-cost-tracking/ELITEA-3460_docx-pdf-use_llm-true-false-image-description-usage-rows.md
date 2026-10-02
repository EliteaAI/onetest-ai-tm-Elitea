---
id: ELITEA-3460
title: "DOCX/PDF with embedded images: use_llm=true produces image-description LLM usage rows; use_llm=false produces none"
priority: medium
type: functional
module: usage-cost-tracking
status: ready
execution_type: manual
tags: [feat:usage-tracking, epic:6566, indexing, use-llm]
requirements: ["EliteaAI/elitea_issues#6566", "EliteaAI/elitea_issues#6571", "EliteaAI/elitea_issues#6607"]
---

# ELITEA-3460: DOCX/PDF with embedded images: use_llm=true produces image-description LLM usage rows; use_llm=false produces none

**Module:** usage-cost-tracking · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that indexing the **same** image-containing DOCX or PDF via the Artifact/SharePoint toolkit with `use_llm=true` produces LLM usage rows (image-description calls, attributed to the correct project/user), while indexing it with `use_llm=false` produces **no** LLM usage row at all (OCR only) — the explicit negative-case test proving the flag gates LLM spend. This is also the primary end-to-end scenario for the Indexing area (replaces the invented "document summarization" scenario).

---

## Preconditions

- Logged in to {{base_url}}.
- Artifact or SharePoint toolkit configured with a bucket.
- A DOCX or PDF file containing at least 2 embedded images, available to index twice (once per `use_llm` setting).

---

## Test Data

| Field | Value |
|-------|-------|
| Document | DOCX or PDF with ≥2 embedded images |
| Run A | `use_llm=true` |
| Run B | `use_llm=false` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Configure the chunking/indexing settings with `use_llm=true` and index the test document (Run A). | Indexing completes; an LLM describes each embedded image (not only the first one). |
| 2 | Inspect `usage_event` for Run A. | LLM usage row(s) for the image-description calls are present, with tokens/cost attributed to the correct project/user. |
| 3 | Verify the indexed content includes the LLM-generated image descriptions (searchable). | Searching for description content returns the indexed document. |
| 4 | Reconfigure with `use_llm=false` and re-index the same document (Run B, treated as a distinct index or reindex depending on environment). | Indexing completes via OCR; no "Transcript is not available" placeholder appears. |
| 5 | Inspect `usage_event` for Run B. | **No** LLM usage row is produced for image handling — only (if any) embedding-call rows for text content. |

---

## Expected Final State

`use_llm=true` produces attributed LLM image-description usage rows; `use_llm=false` on the identical document produces zero such rows.

---

## Pass/Fail Criteria

**Pass:**
- Run A produces correctly attributed LLM usage rows for image descriptions.
- Run B produces no LLM usage rows for image handling.

**Fail:**
- Run A produces no LLM usage row despite images being described.
- Run B still produces an LLM usage row — the flag is not actually gating spend (reportable bug).
