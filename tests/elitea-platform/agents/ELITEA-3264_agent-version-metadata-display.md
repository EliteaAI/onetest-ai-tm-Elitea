---
id: ELITEA-3264
title: "Agent — Version Metadata Display"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3264: Agent — Version Metadata Display

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that each version entry displays all required metadata in the correct format: version name, creation timestamp in format "MMM DD, YYYY, hh:mm AM/PM", and creator information.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions
- Versions created at different times by different users

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions |
| Expected Format | Version name, "MMM DD, YYYY, hh:mm AM/PM", Creator name/email |
| Example | "production-v1", "Jan 15, 2026, 02:30 PM", "Alice Smith (alice@example.com)" |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads successfully |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions with metadata |
| 3 | Select the first version entry and verify it displays version name | Version name is clearly visible (e.g., "production-v1") |
| 4 | Verify the creation timestamp is displayed in correct format | Timestamp displays as "MMM DD, YYYY, hh:mm AM/PM" (e.g., "Jan 15, 2026, 02:30 PM") |
| 5 | Verify the creator name and/or email is displayed | Creator information displays (e.g., "Alice Smith" or "alice@example.com" or both) |
| 6 | Verify timestamp format for multiple versions (check AM/PM, date, time) | All timestamps follow the same format; AM/PM is correct |
| 7 | Verify creator information is displayed consistently across all versions | Creator format is consistent for all versions |
| 8 | Verify metadata does not overlap or cause text truncation issues | All metadata is visible without overlapping or clipping |

## Expected Final State

All version entries display: version name, timestamp in "MMM DD, YYYY, hh:mm AM/PM" format, and creator information, all clearly visible without overlap or truncation.

## Pass/Fail Criteria

**Pass:** All versions display name, correctly formatted timestamp, and creator information; no overlap or truncation; format is consistent

**Fail:** Missing metadata fields; incorrect timestamp format; overlapping text; truncation issues; inconsistent formatting
