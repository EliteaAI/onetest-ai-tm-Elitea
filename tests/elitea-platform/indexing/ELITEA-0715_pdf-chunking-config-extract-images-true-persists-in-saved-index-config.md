---
id: ELITEA-0715
title: "PDF Chunking Config — extract_images=true Persists in Saved Index Configuration"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0715: PDF Chunking Config — extract_images=true Persists in Saved Index Configuration

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a new index is created with `extract_images=true` in the PDF chunking config, the saved index configuration retains this value when viewed in the index configuration panel after indexing.

**Coverage:**
- `extract_images=true` persists in the saved index config view
- Value does not silently revert to `false` after indexing completes
- Config is visible and accurate when navigating to the index configuration panel

## Preconditions

- Artifact Toolkit with a bucket containing at least one file
- Logged into {{base_url}}

## Test Data

- Index Name: `savtest` (7 chars)
- Chunking Config `.pdf` entry: `{ "extract_images": true, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": true }`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new index with Index Name `savtest` and `.pdf` config set to `extract_images: true, use_llm: true`. Click Index. | Indexing starts. |
| 2 | Wait for indexing to complete (✅ Completed). Then click the configuration button on the `savtest` index. | Index configuration view opens. |
| 3 | Inspect the Chunking Config JSON in the configuration view. | `.pdf` entry shows `"extract_images": true`. |
| 4 | Navigate away from the toolkit and return to the same index configuration. | `"extract_images": true` is still displayed — value was not reset. |

## Expected Final State

`"extract_images": true` is still displayed — value was not reset.

## Pass/Fail Criteria

**Pass:**
- `extract_images: true` is present in the saved index config view
- Value persists after navigating away and returning

**Fail:**
- `extract_images` reverts to `false` in the saved config
- Configuration view does not load or shows no chunking config data
