---
id: ELITEA-0714
title: "PDF Chunking Config — Default Value of extract_images is false, Matching .pptx Behavior"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0714: PDF Chunking Config — Default Value of extract_images is false, Matching .pptx Behavior

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the default value of `extract_images` in the `.pdf` chunking config is `false`, matching the `.pptx` default — ensuring no unintentional LLM image extraction occurs on new indexes by default.

**Coverage:**
- `.pdf` `extract_images` defaults to `false`
- `.pptx` `extract_images` also defaults to `false`
- Both configs maintain parity in their default `extract_images` value

## Preconditions

- Any toolkit with indexing support available
- Logged into {{base_url}}

## Test Data

- Expected `.pdf` default: `{ "extract_images": false, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": false }`
- Expected `.pptx` default: `{ "extract_images": false, "max_tokens": 512, "mode": "paged", "pages_per_chunk": 5, "prompt": "", "use_default_prompt": false, "use_llm": false }`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open any toolkit with indexing support → Indexes tab → + (Create New Index). | New Index form opens with Chunking Config field. |
| 2 | Locate the `.pdf` entry in the Chunking Config JSON. Read the value of `extract_images`. | `"extract_images": false` is present. |
| 3 | Locate the `.pptx` entry in the same Chunking Config. Read the value of `extract_images`. | `"extract_images": false` — same default as `.pdf`. |
| 4 | Cancel the index creation without saving. | No index was created; no changes persisted. |

## Expected Final State

No index was created; no changes persisted.

## Pass/Fail Criteria

**Pass:**
- `.pdf` `extract_images` default is `false`
- `.pptx` `extract_images` default is `false`

**Fail:**
- `.pdf` `extract_images` defaults to `true` (would trigger unexpected LLM invocation)
- `extract_images` field is absent from `.pdf` entry
