---
id: ELITEA-0242
title: "[#4919] New Wiki Generation Writes to `wiki-artifacts` Bucket"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:artifacts, int:deepwiki, issue:4919, migration, r-2.0.3]
requirements: [4919]
---
# ELITEA-0242: [#4919] New Wiki Generation Writes to `wiki-artifacts` Bucket

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the new DeepWiki code is deployed, newly generated wikis are written to the `wiki-artifacts` bucket (not the old `wiki_artifacts`). This covers the write path: K8s worker pod env var `DEEPWIKI_ARTIFACT_BUCKET=wiki-artifacts`, `WikiRegistryManager`, `WikiLoader`, and all generation agents that previously hardcoded `wiki_artifacts`.

## Preconditions

New DeepWiki code deployed (all DEFAULT_BUCKET references updated to 'wiki-artifacts')
A GitHub/GitLab repository is accessible for wiki generation
Artifact Toolkit accessible to verify bucket contents

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger a new wiki generation for a repository via the DeepWiki application. | Wiki generation starts. K8s worker pod is launched with DEEPWIKI_ARTIFACT_BUCKET=wiki-artifacts. |
| 2 | Wait for generation to complete. Using Artifact Toolkit `list_files` on `wiki-artifacts`, verify new files are present (manifests, indexes, pages under the new wiki ID). | New wiki files appear in `wiki-artifacts`. No files written to the old `wiki_artifacts` bucket for the new wiki. |
| 3 | Call `list_wikis` and confirm the newly generated wiki appears. | New wiki is listed and accessible. |
| 4 | Call `resolve_and_ask` on the newly generated wiki. | Wiki answers questions correctly. Content is served from `wiki-artifacts`. |

## Expected Final State

Wiki answers questions correctly. Content is served from `wiki-artifacts`.

## Pass/Fail Criteria

New wiki files present in wiki-artifacts after generation
No new files written to wiki_artifacts for newly generated wikis
list_wikis shows the new wiki
resolve_and_ask works on the newly generated wiki
