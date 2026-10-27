---
id: ELITEA-3820
title: "SonarQube Credential URL Normalization - Chat Runtime (No Test Connection)"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

# ELITEA-3820: SonarQube Credential URL Normalization - Chat Runtime

**Module:** toolkits-credentials · **Priority:** critical · **Type:** functional

**Objective:** Verify that SonarQube credentials accept URLs with trailing slashes (Test Connection is not available), normalize them server-side, and work correctly in Chat runtime execution.

**Note:** Test Connection is NOT available for SonarQube credentials - this is expected behavior. URL normalization is verified only at runtime.

---

## Preconditions

- User is logged in to the Elitea platform
- User has access to Credentials, Toolkits & Indexes, and Chat sections
- Valid SonarCloud or SonarQube credentials are available (API token)
- URL: `https://sonarcloud.io`

---

## Test Data

| Field | Value |
|-------|-------|
| Credential Display Name | autotest_sonar_trailing_slash |
| Credential ID | autotest-sonar-trailing-slash |
| URL | `https://sonarcloud.io/` (with single trailing slash) |
| Sonar Token | Valid SonarCloud API token (format: `squ_...`) |
| Toolkit Name | autotest_sonar_toolkit |

---

## Steps

### Part 1: Create Credential with trailing slash

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button | Credential type selection dialog opens |
| 3 | Select "Sonar" credential type | New Sonar Credential form opens |
| 4 | Enter Display Name: "autotest_sonar_trailing_slash" | Field accepts input |
| 5 | Enter ID: "autotest-sonar-trailing-slash" | Field accepts input |
| 6 | Enter URL WITH trailing slash: `https://sonarcloud.io/` | Field accepts URL with trailing slash, slash remains visible |
| 7 | Enter valid SonarCloud token (format: `squ_...`) | Field accepts input |
| 8 | Observe "Test connection" button state | **Expected:** Button is disabled or shows "Test connection is not available for this credential type" |
| 9 | Click "Save" button | Success notification: "Credential saved successfully" |
| 10 | Verify credential appears in list | "autotest_sonar_trailing_slash" visible in credentials list with Sonar badge |

### Part 2: Create Toolkit

| # | Action | Expected Result |
|---|--------|-----------------|
| 11 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 12 | Click "+ Toolkit" button | Toolkit type selection dialog opens |
| 13 | Select "Sonar" toolkit type | New Sonar Toolkit form opens |
| 14 | Enter Toolkit Name: "autotest_sonar_toolkit" | Field accepts input |
| 15 | In "Sonar Configuration" dropdown, select "autotest_sonar_trailing_slash" | Credential is selected, form shows credential details |
| 16 | Click "Save" button | Success notification: "Toolkit saved successfully" |
| 17 | Verify toolkit appears in list | "autotest_sonar_toolkit" visible in toolkits list |

### Part 3: Verify Runtime in Chat

| # | Action | Expected Result |
|---|--------|-----------------|
| 18 | Navigate to Chat section | Chat page loads successfully |
| 19 | Start a new chat conversation | New chat session opened |
| 20 | Attach "autotest_sonar_toolkit" to Chat | Toolkit attached, visible in Chat |
| 21 | Send message: "what can I do with the help of attached toolkit? does it connect?" | AI responds: "Yes—the attached toolkit is connected and responding" |
| 22 | Verify toolkit capabilities are listed | Available tools displayed (e.g., get_sonar_data) |
| 23 | Send message: "Get projects list" or similar SonarQube query | AI processes and invokes SonarQube toolkit |
| 24 | Observe toolkit execution | Toolkit invoked, execution completes |
| 25 | Verify response | Valid response displayed (data or "organization required" message) |
| 26 | Verify no URL-related error messages | No errors about malformed URLs, double slashes, or trailing slashes |

---

## Expected Final State

- SonarQube credential is saved with trailing slash visible in URL field
- Test Connection is NOT available (expected for Sonar)
- Toolkit successfully references the credential
- Chat confirms toolkit is "connected and responding"
- Toolkit can be invoked without URL-related errors
- API endpoint construction is correct (no double slashes)

---

## Pass/Fail Criteria

**Pass:**
- URL field accepts trailing slash and keeps it visible in UI
- Test Connection button is disabled/unavailable (expected behavior)
- Credential saves successfully without Test Connection
- Toolkit successfully links to credential
- Chat confirms: "attached toolkit is connected and responding"
- Toolkit tools are available and can be invoked
- No URL-related error messages during runtime
- API calls use correctly normalized URLs

**Fail:**
- URL field rejects or strips trailing slash in UI
- Test Connection becomes required (should be unavailable)
- Credential fails to save
- Toolkit cannot reference credential
- Toolkit fails to connect in Chat runtime
- URL-related error messages appear during tool invocation
- Malformed API URLs with double slashes

---

## Cleanup

- Delete Toolkit "autotest_sonar_toolkit"
- Delete Credential "autotest_sonar_trailing_slash"
