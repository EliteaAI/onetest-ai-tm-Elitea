---
id: ELITEA-0712
title: "PDF Chunking Config UI — extract_images Field Present in Create New Index Form"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4788]
---
# ELITEA-0712: PDF Chunking Config UI — extract_images Field Present in Create New Index Form

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the `.pdf` entry in the Chunking Config JSON editor of the Create New Index form includes the `extract_images` parameter after the fix, consistent with the `.pptx` config.

**Coverage:**
- `extract_images` field present in `.pdf` chunking config in Artifact Toolkit index creation
- `extract_images` field present in `.pdf` chunking config in SharePoint Toolkit index creation
- Field value defaults to `false`
- `.pdf` config contains all five fields: `extract_images`, `max_tokens`, `prompt`, `use_default_prompt`, `use_llm`

## Preconditions

- Logged into {{base_url}}
- Private project context selected
- At least one Artifact Toolkit and one SharePoint Toolkit exist with indexing enabled

## Test Data

- Expected `.pdf` default config: `{ "extract_images": false, "max_tokens": 512, "prompt": "", "use_default_prompt": false, "use_llm": false }`
- Expected `.pptx` default config: `{ "extract_images": false, "max_tokens": 512, "mode": "paged", "pages_per_chunk": 5, "prompt": "", "use_default_prompt": false, "use_llm": false }`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits from the sidebar. Open an Artifact Toolkit → Indexes tab → click the + button (Create New Index). | New Index form opens with Index Name, Clean Index, Progress Step, and Chunking Config fields visible. |
| 2 | Scroll to the Chunking Config JSON editor. Locate the `.pdf` entry in the JSON. | `.pdf` entry is visible in the Chunking Config JSON. |
| 3 | Check that the `.pdf` entry contains the key `"extract_images"` with value `false`. | `"extract_images": false` is present in the `.pdf` config block. |
| 4 | Verify all other `.pdf` fields are also present: `max_tokens`, `prompt`, `use_default_prompt`, `use_llm`. | All five fields are present for `.pdf` — `extract_images`, `max_tokens`, `prompt`, `use_default_prompt`, `use_llm`. |
| 5 | Cancel the index creation. Navigate to a SharePoint Toolkit → Indexes tab → + Create New Index. Inspect the `.pdf` entry in the Chunking Config. | The same `.pdf` config with `extract_images` is shown in the SharePoint Toolkit as well. |

## Expected Final State

The same `.pdf` config with `extract_images` is shown in the SharePoint Toolkit as well.

## Pass/Fail Criteria

**Pass:**
- `.pdf` entry contains `"extract_images": false`
- All existing `.pdf` fields remain present and unchanged
- Both Artifact Toolkit and SharePoint Toolkit show the field

**Fail:**
- `extract_images` is absent from `.pdf` chunking config
- `.pdf` config is broken or produces invalid JSON
- Field is present in one toolkit type but not the other
