---
id: ELITEA-3815
title: "Credentials UI behavior for credential URL configuration with trailing slashes"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Credentials and Toolkits & Indexes sections

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test URL with trailing slash | `https://jiraeu.epam.com/` |
| Test URL without trailing slash | `https://jiraeu.epam.com` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" and select Jira credential type | Credential configuration form opens |
| 3 | Click in Base URL input field | Field is focused, ready for input |
| 4 | Type URL with trailing slash: `https://jiraeu.epam.com/` | Field accepts input character by character, no client-side validation preventing trailing slash |
| 5 | Verify trailing slash is visible in field | URL with trailing slash displayed: `https://jiraeu.epam.com/` |
| 6 | Enter Display Name and valid credentials | All required fields populated |
| 7 | Click "Check Connection" button | Button becomes disabled or shows loading state |
| 8 | Observe loading indicator during connection check | Loading spinner or progress indicator displayed |
| 9 | Wait for connection check to complete | Connection check completes (URL normalized server-side) |
| 10 | Verify success message displayed | Clear success message: "Connection successful" or similar |
| 11 | Verify success message does NOT mention URL normalization | Message is user-friendly, no technical details about trailing slash removal |
| 12 | Click "Save" to save credential | Save button triggered |
| 13 | Verify credential saved successfully | Success notification displayed |
| 14 | Close and reopen the same credential configuration | Credential form opens with saved values |
| 15 | Check Base URL field content | URL may be displayed as originally entered or normalized (implementation dependent, both acceptable) |
| 16 | Edit Base URL to remove trailing slash: `https://jiraeu.epam.com` | Field updates |
| 17 | Click "Check Connection" again | Connection check runs |
| 18 | Verify connection succeeds identically to version with trailing slash | Success message displayed, behavior identical |

## Expected Final State

- Credentials UI accepts URLs with trailing slashes in input field
- No client-side validation prevents entering trailing slashes
- Check Connection button shows appropriate loading state
- Success/error messages are clear and user-friendly
- Configuration save/reload workflow works correctly
- UI behavior is consistent whether URL has trailing slash or not

## Pass/Fail Criteria

**Pass:**
- URL input field accepts trailing slashes without client-side errors
- Trailing slash is visible in input field as user types
- "Check Connection" button shows loading state during check
- Success message is clear and user-friendly (no technical jargon about URL normalization)
- Configuration saves successfully with URL in any format
- Reload of configuration displays URL correctly
- UI is responsive and provides feedback for all actions
- Behavior is identical for URLs with and without trailing slashes

**Fail:**
- URL input field rejects or strips trailing slash on client-side
- No loading indicator during connection check
- Success/error messages are confusing or technical
- Configuration fails to save
- UI freezes or becomes unresponsive
- Inconsistent behavior between URLs with/without trailing slashes
- Poor user experience (no feedback, unclear states)
