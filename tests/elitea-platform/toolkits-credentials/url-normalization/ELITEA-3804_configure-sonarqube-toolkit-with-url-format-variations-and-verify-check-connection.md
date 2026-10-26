---
id: ELITEA-3804
title: "Configure SonarQube credential with URL variations and verify runtime execution in Chat"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to Credentials, Toolkits & Indexes, and Chat sections
- Valid SonarQube or SonarCloud credentials are available (token)

## Note

**Test Connection is not available for SonarQube credentials** - this is expected behavior. Connection validation happens at runtime when toolkit is used.

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| SonarQube URL variant 1 | `https://sonarcloud.io` (no trailing slash) |
| SonarQube URL variant 2 | `https://sonarcloud.io/` (single trailing slash) |
| SonarQube URL variant 3 | `https://sonarcloud.io///` (multiple trailing slashes) |
| SonarQube token | Valid SonarCloud authentication token (format: `squ_...`) |
| SonarQube organization | Your SonarCloud organization key (for Chat query) |

## Steps

### Part 1: Create Credential with URL variations

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button and select "Sonar" | New Sonar Credential form opens |
| 3 | Enter Display Name: "test 1 Sonar" | Display Name field accepts the input |
| 4 | Enter ID (auto-generated): "test_1_sonar" | ID field accepts the input |
| 5 | Enter URL WITHOUT trailing slash: `https://sonarcloud.io` | URL field accepts the input |
| 6 | Enter valid SonarCloud token (format: `squ_...`) | Sonar Token field accepts the input |
| 7 | Observe that "Test connection" button is disabled or shows "not available" message | **Expected:** Test connection is not available for this credential type |
| 8 | Click "Save" button | Credential saved successfully |
| 9 | Edit the same Sonar credential | Credential form opens with saved values |
| 10 | Change URL to include single trailing slash: `https://sonarcloud.io/` | URL field accepts the input with trailing slash |
| 11 | Verify trailing slash is visible in URL field | URL displayed as entered: `https://sonarcloud.io/` |
| 12 | Click "Save" button | Credential saved successfully |
| 13 | Edit the credential again | Credential form opens |
| 14 | Change URL to include multiple trailing slashes: `https://sonarcloud.io///` | URL field accepts the input |
| 15 | Verify multiple trailing slashes are visible | URL displayed as entered: `https://sonarcloud.io///` |
| 16 | Click "Save" button | Credential saved successfully |

### Part 2: Create Toolkit

| # | Action | Expected Result |
|---|--------|-----------------|
| 17 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 18 | Click "+ Toolkit" button and select "Sonar" | New Sonar Toolkit form opens |
| 19 | Enter Toolkit Name: "test 1 Sonar" | Toolkit Name field accepts the input |
| 20 | In "Sonar Configuration" dropdown, select credential "test 1 Sonar" | Credential is selected successfully |
| 21 | Click "Save" button | Toolkit saved successfully and linked to credential |

### Part 3: Verify runtime execution in Chat

| # | Action | Expected Result |
|---|--------|-----------------|
| 22 | Navigate to Chat interface | Chat page loads successfully |
| 23 | Attach "test 1 Sonar" toolkit to Chat | Toolkit attached, visible in Chat |
| 24 | Send message: "what can I do with the help of attached toolkit? does it connect?" | Message sent, AI processes |
| 25 | Observe Chat response | Chat responds: "Yes—the attached toolkit is connected and responding" (or similar confirmation) |
| 26 | Verify toolkit shows available tools (e.g., get_sonar_data) | Available capabilities listed in Chat |
| 27 | Send query using SonarQube data (e.g., "Get projects list" or similar simple query) | Message sent |
| 28 | Observe toolkit invocation | Chat shows toolkit invoked, execution completes |
| 29 | Verify response contains data or appropriate message | Valid response displayed (data or "organization required" message) |
| 30 | Verify no URL-related error messages appear | No errors about malformed URLs, double slashes, or trailing slashes |

## Expected Final State

- SonarQube credential is configured and saved successfully with URL containing trailing slashes (UI keeps trailing slashes visible)
- SonarQube toolkit is created and linked to the credential successfully
- Test Connection is not available for Sonar credentials (expected behavior)
- Toolkit connects and responds successfully in Chat runtime
- URL normalization happens server-side before API calls
- No error messages related to trailing slashes or malformed URLs during runtime execution

## Pass/Fail Criteria

**Pass:**
- Sonar credential accepts URL with and without trailing slashes (all three variations)
- Trailing slashes remain visible in URL field as entered (not stripped by UI)
- Test Connection button is disabled/unavailable (expected for Sonar)
- Credential saves successfully with all URL format variations
- Toolkit successfully references the credential
- Toolkit connects and responds in Chat: "attached toolkit is connected and responding"
- Toolkit tools (e.g., get_sonar_data) are available and can be invoked
- No URL-related error messages during runtime execution
- API path concatenation works correctly (no double slashes in API calls)

**Fail:**
- URL field rejects trailing slashes
- Test Connection becomes required (should be unavailable for Sonar)
- Credential fails to save with any URL format variation
- Toolkit cannot reference the credential
- Toolkit fails to connect in Chat runtime
- URL-related error messages appear during tool invocation
- Malformed API URLs with double slashes are generated in API calls
