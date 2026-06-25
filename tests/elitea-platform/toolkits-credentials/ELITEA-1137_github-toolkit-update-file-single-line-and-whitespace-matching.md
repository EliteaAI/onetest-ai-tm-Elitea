---
id: ELITEA-1137
title: "GitHub Toolkit - update_file Single-line and Whitespace Matching"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [backend, toolkit, github, sdk]
requirements: []
---
# ELITEA-1137: GitHub Toolkit - update_file Single-line and Whitespace Matching

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that `update_file` tool in GitHub toolkit (and other repository toolkits) correctly handles single-line content replacements and whitespace-tolerant matching.

## Preconditions

- User logged in to Elitea stage environment
- GitHub credentials configured
- Test repository available with write access
- Understanding of GitHub toolkit `update_file` tool

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create test file `test.txt` in repo with content: `line1\nline2\n` | File created successfully |
| 2 | Use GitHub toolkit `update_file` tool with: file_path='test.txt', old_string='line1', new_string='LINE1' | Tool returns success, file content updated to `LINE1\nline2\n` |
| 3 | Verify file content in repository | File contains `LINE1\nline2\n` |
| 4 | Create test file `whitespace.txt` with content: `  hello  world  \n` | File created successfully |
| 5 | Use `update_file` tool with: file_path='whitespace.txt', old_string='hello world', new_string='HELLO WORLD' | Tool returns success (whitespace normalized), file updated |
| 6 | Verify file content | File contains `HELLO WORLD` (whitespace normalized) |
| 7 | Create test file `multiline.txt` with content: `line1\nline2\nline3\n` | File created successfully |
| 8 | Use `update_file` tool with: old_string='line1\nline2', new_string='LINE1\nLINE2' | Tool returns success, file updated |
| 9 | Verify file content | File contains `LINE1\nLINE2\nline3\n` (multi-line baseline works) |

## Expected Final State

File contains `LINE1\nLINE2\nline3\n` (multi-line baseline works)

## Pass/Fail Criteria

PASS: All three test cases succeed - single-line, whitespace-tolerant, and multi-line replacements work
FAIL: Test Case 1 or Test Case 2 fails with 'content not found' error
