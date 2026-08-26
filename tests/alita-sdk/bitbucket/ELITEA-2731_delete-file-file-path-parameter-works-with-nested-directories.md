---
id: ELITEA-2731
title: "BitBucket - delete_file: file_path parameter works with nested directories"
priority: high
type: functional
module: bitbucket
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, bitbucket, file-operations, issue:3401]
requirements: [EliteaAI/elitea_issues#3401]
---
# ELITEA-2731: BitBucket - delete_file: file_path parameter works with nested directories

**Module:** Bitbucket · **Priority:** High · **Type:** Functional

**Objective:** Verify `delete_file` can delete files located in nested directory structures.

## Preconditions

BitBucket toolkit configured with write/delete permissions.

## Test Data

| Scenario | File Path |
|----------|-----------|
| Single level | "src/helper.js" |
| Multiple levels | "src/components/utils/validator.py" |
| Deep nesting | "docs/api/v2/endpoints/users.md" |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Create file at "src/helper.js" in main branch | File exists in nested directory |
| 2 | Call `delete_file` with file_path="src/helper.js", branch_name="main" | File is deleted |
| 3 | Verify parent directory "src/" still exists | Directory remains intact |
| 4 | Create file at "src/components/utils/validator.py" | File exists in deeply nested directory |
| 5 | Call `delete_file` with file_path="src/components/utils/validator.py", branch_name="main" | File is deleted |
| 6 | Verify parent directories remain and other files in "src/" are unaffected | Only target file is deleted |
| 7 | Create file at "docs/api/v2/endpoints/users.md" | File exists in deep nesting |
| 8 | Call `delete_file` with file_path="docs/api/v2/endpoints/users.md", branch_name="main" | File is deleted |
| 9 | Verify all parent directories remain intact | Directory structure preserved |

## Expected Final State

All files in nested directories are successfully deleted, parent directories remain intact, other files in same directories are unaffected.

## Pass/Fail Criteria

**Pass:**
- All nested files are successfully deleted
- Parent directories remain intact
- Other files in same directories are unaffected

**Fail:**
- Any nested file fails to delete
- Parent directories are removed
- Other files in same directories are affected
