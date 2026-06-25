---
id: ELITEA-1765
title: "Test Bare personality with custom instructions over 2000 characters"
priority: high
type: functional
module: chat
status: draft
execution_type: manual
tags: [feat:personalization, r-2.0.4, personality, bare-persona, edge-case, limits]
requirements: [EliteaAI/elitea_issues#5264]
---
# ELITEA-1765: Test Bare personality with custom instructions over 2000 characters

**Module:** Chat · **Priority:** High · **Type:** Functional

**Objective:** Verify that Bare personality handles custom instructions over 2000 characters correctly

## Preconditions

- User is logged into EliteA platform
- User can create new conversations
- Bare personality available in dropdown
- Custom instructions field character limit known or testable

## Test Data

- Custom instructions: (2500+ character text with specific formatting and tone guidelines)
- Example long instructions: "You are a senior software architect. When answering questions: 1. Always start with a high-level overview... [continue with detailed, structured instructions totaling 2500+ characters]"

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create new conversation | New conversation opens |
| 2 | Open Context Management modal | Modal opens |
| 3 | Select "Bare" personality | Bare selected |
| 4 | Verify custom instructions field appears | Field visible |
| 5 | Prepare 2500+ character custom instructions text | Text ready to paste |
| 6 | Paste or type long custom instructions | Text appears in field |
| 7 | Verify character counter (if present) | Counter shows 2500+ characters |
| 8 | Check for validation warnings or errors | Note any character limit warnings |
| 9 | Attempt to apply changes | System response noted (acceptance or rejection) |
| 10 | If accepted: verify instructions saved | Settings saved successfully |
| 11 | If rejected: note error message and max limit | Error message clear and helpful |
| 12 | If accepted: send test message | Response received |
| 13 | Verify response follows long custom instructions | Instructions applied correctly |
| 14 | Reopen Context Management modal | Modal opens |
| 15 | Verify custom instructions preserved | Full text or truncated text displayed based on system limit |

## Expected Final State

- System has defined character limit for custom instructions
- Limit is enforced with clear validation message
- If limit allows 2500+: long instructions work correctly
- If limit restricts: error message is clear and helpful
- System behavior is predictable and documented
- No data corruption or system errors

## Pass/Fail Criteria

**Pass:**
- Character limit clearly defined and enforced
- Validation message clear if limit exceeded
- If within limit: long instructions work correctly
- If over limit: graceful rejection with helpful error
- System handles edge case predictably
- No crashes or data corruption

**Fail:**
- No character limit or unclear limit
- Instructions silently truncated without warning
- System crashes or errors with long input
- Instructions corrupted or lost
- Validation messages unclear or missing
- Unpredictable or inconsistent behavior
