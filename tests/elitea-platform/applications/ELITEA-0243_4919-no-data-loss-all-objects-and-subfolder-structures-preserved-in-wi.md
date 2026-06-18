---
id: ELITEA-0243
title: "[EliteaAI/elitea_issues#4919] No Data Loss — All Objects and Subfolder Structures Preserved in `wiki-artifacts` After Migration"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:artifacts, data-integrity, int:deepwiki, issue:4919, migration, r-2.0.3]
requirements: [4919]
---
# ELITEA-0243: [EliteaAI/elitea_issues#4919] No Data Loss — All Objects and Subfolder Structures Preserved in `wiki-artifacts` After Migration

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that the admin migration task copies all objects from `wiki_artifacts` to `wiki-artifacts` without data loss. File counts, subfolder structures (wiki IDs, `/indexes/`, `/wiki_pages/`, `/wiki_manifest_*.json`, `_registry/wikis.json`), and file content must all match between old and new buckets.

## Preconditions

At least one project with multiple wikis and nested subfolders in `wiki_artifacts`
Admin migration task has been run (project_id=all, no dry_run flag)
Artifact Toolkit accessible for both old and new buckets

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Before migration (or using a record of pre-migration state): use Artifact Toolkit `list_files` on `wiki_artifacts` and note the total object count and directory structure (wiki IDs, subfolder paths). | Baseline object list and count recorded from `wiki_artifacts`. |
| 2 | After migration task completes, use Artifact Toolkit `list_files` on `wiki-artifacts` and record the total object count and directory structure. | Object count and directory structure in `wiki-artifacts` matches the baseline from `wiki_artifacts`. All wiki IDs, `/indexes/`, `/wiki_pages/`, manifest files, and `_registry/wikis.json` are present. |
| 3 | Spot-check 2-3 specific files: download the same file from both buckets and compare content. | File content is identical between old and new bucket. No corruption during copy. |
| 4 | Verify the migration summary/log from the admin task output. | Migration log reports 0 copy errors. All projects show success. Sentinel `_migration/bucket_rename_done` present for each migrated project. |

## Expected Final State

Migration log reports 0 copy errors. All projects show success. Sentinel `_migration/bucket_rename_done` present for each migrated project.

## Pass/Fail Criteria

Object count in wiki-artifacts equals object count in wiki_artifacts (pre-migration)
All subfolder structures preserved (wiki IDs, /indexes/, /wiki_pages/)
_registry/wikis.json present and content-identical
Spot-checked file content matches between old and new bucket
Migration log shows 0 errors
Sentinel _migration/bucket_rename_done present for each project
