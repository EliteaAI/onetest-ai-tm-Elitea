---
id: ELITEA-0246
title: "[EliteaAI/elitea_issues#4919] Artifact Toolkit Can Access `wiki-artifacts` Bucket After Migration"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:artifacts, int:deepwiki, issue:4919, migration, r-2.0.3]
requirements: [4919]
---
# ELITEA-0246: [EliteaAI/elitea_issues#4919] Artifact Toolkit Can Access `wiki-artifacts` Bucket After Migration

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the `wiki_artifacts` → `wiki-artifacts` bucket rename, the Artifact Toolkit can successfully access and operate on files in the `wiki-artifacts` bucket. The hyphenated bucket name must pass the Artifacts API validation regex (`^[a-z][a-z0-9-]*$`) which previously rejected underscored names.

## Preconditions

DeepWiki plugin upgraded to new version (code references `wiki-artifacts`)
Admin migration task has been run for the target project
`wiki-artifacts` bucket exists with migrated content
Artifact Toolkit configured and accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Using the Artifact Toolkit (via Agent Chat or Toolkit Test Settings), call `list_files` targeting the `wiki-artifacts` bucket. | `list_files` executes successfully. Files are returned from the `wiki-artifacts` bucket. No validation error about bucket name format. |
| 2 | Call `read_file` on a known file in the `wiki-artifacts` bucket (e.g., a wiki manifest or index file). | File content is returned successfully. No 'bucket not found' or access error. |
| 3 | Upload a test file to the `wiki-artifacts` bucket via the Artifact Toolkit `createFile` tool. | File is uploaded successfully to `wiki-artifacts`. The bucket name with hyphen is accepted without modification or error. |

## Expected Final State

File is uploaded successfully to `wiki-artifacts`. The bucket name with hyphen is accepted without modification or error.

## Pass/Fail Criteria

list_files returns files from wiki-artifacts without error
read_file retrieves file content from wiki-artifacts
createFile succeeds — no bucket name validation error
No reference to old wiki_artifacts bucket in any tool response
