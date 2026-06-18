---
id: ELITEA-0244
title: "[EliteaAI/elitea_issues#4919] Pre-Migration Wikis Load Correctly After Code Deployment (Fallback Read from `wiki_artifacts`)"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:artifacts, int:deepwiki, issue:4919, migration, fallback, r-2.0.3]
requirements: [4919]
---
# ELITEA-0244: [EliteaAI/elitea_issues#4919] Pre-Migration Wikis Load Correctly After Code Deployment (Fallback Read from `wiki_artifacts`)

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that during the transition window — after new DeepWiki code is deployed (reads `wiki-artifacts` first) but before the admin migration task has run (data still in `wiki_artifacts` only) — existing pre-migration wikis still load correctly via the fallback read path. The fallback in `ArtifactManager._fetch_latest_manifest()` and `WikiRegistryManager.load_registry()` must retry in `wiki_artifacts` when the object is not found in `wiki-artifacts`.

## Preconditions

New DeepWiki code is deployed (DEFAULT_BUCKET = 'wiki-artifacts')
Admin migration task has NOT yet been run
At least one wiki exists with data in the old `wiki_artifacts` bucket
`wiki-artifacts` bucket does not yet exist or is empty for this project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a DeepWiki application that has pre-existing wikis generated before the code upgrade. Call `list_wikis` tool. | Previously generated wikis are listed correctly. The fallback path reads from `wiki_artifacts` since `wiki-artifacts` is empty or missing. No 'manifest not found' or empty response. |
| 2 | Call `resolve_and_ask` on one of the pre-migration wikis with a test question. | Wiki content is retrieved and a coherent answer is returned. DeepWiki resolves the manifest from the old `wiki_artifacts` bucket via the fallback path. |
| 3 | Call `resolve_and_deep_research` on the same wiki. | Deep research completes successfully using data from the old bucket. No errors related to bucket name or missing files. |

## Expected Final State

Deep research completes successfully using data from the old bucket. No errors related to bucket name or missing files.

## Pass/Fail Criteria

list_wikis returns pre-migration wikis without error
resolve_and_ask returns a valid answer from pre-migration wiki content
resolve_and_deep_research completes without bucket-related errors
No user-visible error or empty response during the transition window
