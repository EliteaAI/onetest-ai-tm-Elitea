---
id: ELITEA-1655
title: "SR03 - Special Characters"
priority: high
type: functional
module: state-retrieval
status: ready
execution_type: automated
tags: [state_retrieval, special_chars, code_node, unicode]
requirements: []
---
# ELITEA-1655: SR03 - Special Characters

**Module:** State Retrieval · **Priority:** High · **Type:** Functional

**Objective:** Verify quotes, backslashes, and unicode characters in state string variables are handled correctly in code nodes.

## Preconditions

Pipeline engine is running and accessible
No LLM node required (code node only)
No external toolkit or service credentials required
Test pipeline: suites/state_retrieval/tests/test_case_3_special_characters.yaml

## Test Data

sql_query: "SELECT * FROM users WHERE name = 'John' AND status = \"active\""
file_path: "C:\\Users\\admin\\file.txt"
unicode_text: "Привет мир! 你好世界 🎉"
regex_pattern: "^\\d+\\.\\d+$"
Entry point: verify_special_chars (code node)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Initialize pipeline state with 4 string variables containing special characters: SQL query with both quote types, Windows file path with backslashes, unicode text (Cyrillic, Chinese, emoji), regex pattern with escaped chars | State is initialized; all special characters preserved as-is in state variables |
| 2 | Execute code node 'verify_special_chars'; reads all 4 vars from alita_state | All 4 variables are retrieved as Python str type |
| 3 | Code checks SQL query contains both single quote (') and double quote (") characters | sql_has_quotes=True; both quote types preserved |
| 4 | Code checks file_path contains backslash character (chr(92)) | path_has_backslash=True; Windows path separators not modified |
| 5 | Code checks unicode_text contains 'Привет' (Cyrillic) and emoji 🎉 (chr(127881)) | unicode_preserved=True; all Unicode codepoints intact |
| 6 | Code compares regex_pattern against expected escaped form: ^\d+\.\d+$ | regex_correct=True; escape sequences not double-escaped |
| 7 | Verify test_results.test_passed from code node output | test_results.test_passed=True; all 4 special-char checks True |

## Expected Final State

test_results.test_passed=True; all 4 special-char checks True

## Pass/Fail Criteria

PASS: test_passed=True and all 4 checks True
FAIL: Quote characters are escaped or removed in SQL string
FAIL: Backslashes in file path are doubled or removed
FAIL: Unicode characters are replaced with escape sequences or dropped
FAIL: Regex pattern escape sequences are double-escaped
