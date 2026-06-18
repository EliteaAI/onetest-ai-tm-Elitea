---
id: ELITEA-0245
title: "[EliteaAI/elitea_issues#4919] Pre-Migration Wikis Load Correctly After Data Migration (From New `wiki-artifacts` Bucket)"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:artifacts, int:deepwiki, issue:4919, migration, r-2.0.3]
requirements: [4919]
---
# ELITEA-0245: [EliteaAI/elitea_issues#4919] Pre-Migration Wikis Load Correctly After Data Migration (From New `wiki-artifacts` Bucket)

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the admin migration task has run and all data has been copied from `wiki_artifacts` to `wiki-artifacts`, existing pre-migration wikis continue to load correctly — this time reading from the new bucket, not the fallback. The sentinel `_migration/bucket_rename_done` should be present and no fallback to the old bucket should be necessary.

## Preconditions

New DeepWiki code is deployed (DEFAULT_BUCKET = 'wiki-artifacts')
Admin migration task has been run with project_id=all (no dry_run)
Sentinel object `_migration/bucket_rename_done` exists in `wiki-artifacts` for the test project
Pre-migration wikis were present in `wiki_artifacts` before migration

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm migration completed: use Artifact Toolkit `list_files` on `wiki-artifacts` and verify the sentinel file `_migration/bucket_rename_done` is present alongside wiki content. | Sentinel file present. Wiki files (manifests, indexes, pages) visible in `wiki-artifacts`. |
| 2 | Call `list_wikis` on the DeepWiki application. | All pre-migration wikis are listed. Content is served from the new `wiki-artifacts` bucket. |
| 3 | Call `resolve_and_ask` on a pre-migration wiki with a question that was answerable before migration. | The same answer is returned as before migration. No data loss. Content integrity preserved. |
| 4 | Call `delete_wiki` on one of the migrated wikis. | Wiki is deleted from `wiki-artifacts`. `list_wikis` no longer shows the deleted wiki. No error about the wiki being in the wrong bucket. |

## Expected Final State

Wiki is deleted from `wiki-artifacts`. `list_wikis` no longer shows the deleted wiki. No error about the wiki being in the wrong bucket.

## Pass/Fail Criteria

Sentinel _migration/bucket_rename_done present in wiki-artifacts
list_wikis returns all pre-migration wikis
resolve_and_ask answer matches pre-migration behavior
delete_wiki removes wiki from new bucket without error
No fallback to wiki_artifacts needed after migration
