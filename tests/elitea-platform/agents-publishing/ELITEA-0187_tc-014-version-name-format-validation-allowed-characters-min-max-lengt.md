---
id: ELITEA-0187
title: "TC-014: Version Name Format Validation (Allowed Characters, Min/Max Length, Trailing Spaces)"
priority: high
type: functional
module: agents-publishing
status: draft
execution_type: manual
tags: [feat:agents, story:3772, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3772]
---
# ELITEA-0187: TC-014: Version Name Format Validation (Allowed Characters, Min/Max Length, Trailing Spaces)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that version name input enforces the allowed character set (alphanumeric, dots, hyphens, underscores), 1–50 character length limit, whitespace trimming, and rejects empty or invalid inputs.

Coverage:
- Valid formats accepted: v1.0, v2.0-stable, release_2025.01, single char, 50-char max
- Disallowed characters rejected: spaces within name, !, @, #, etc.
- Max 50 characters enforced
- Empty / whitespace-only rejected
- Leading/trailing spaces trimmed

## Preconditions

- Logged in as User A; Publish modal open on Agent C

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Publish modal on Agent C | Modal with Version Name field open |
| 2 | Leave Version Name empty; check checkbox | Continue button remains disabled; empty not accepted |
| 3 | Enter '   ' (spaces only); check checkbox | Continue button remains disabled or error shown |
| 4 | Enter 'v1.0 release!' (space + !); check checkbox | Validation error for invalid characters; Continue button disabled |
| 5 | Enter the 51-character string; check checkbox | Input rejected, truncated, or length error shown |
| 6 | Enter '  v1.0  ' (with surrounding spaces); check checkbox | Accepted; value treated as 'v1.0' after trimming |
| 7 | Enter each valid format (v1.0, v2.0-stable, release_2025.01, single char, 50-char max) one by one; check checkbox | Each valid entry enables the Continue button with no error |

## Expected Final State

Each valid entry enables the Continue button with no error

## Pass/Fail Criteria

PASS:
- All valid formats in the test data table are accepted
- Whitespace-only, invalid characters, and >50 char strings are rejected with informative feedback
- Leading/trailing spaces are trimmed silently

FAIL:
- Invalid characters (spaces within name, !, @) are accepted
- Empty or whitespace-only version name enables the Continue button
- Version name exceeding 50 chars is silently accepted without any truncation or error
