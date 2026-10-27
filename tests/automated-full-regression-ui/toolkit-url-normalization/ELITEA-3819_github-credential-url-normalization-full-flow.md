---
id: ELITEA-3819
title: "GitHub Credential URL Normalization - Full Flow with Chat"
priority: critical
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:toolkits, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6810]
---

# ELITEA-3819: GitHub Credential URL Normalization - Full Flow with Chat

**Module:** toolkits-credentials · **Priority:** critical · **Type:** functional

**Objective:** Verify that GitHub credentials accept Base URLs with trailing slashes, normalize them server-side, and work correctly in Chat runtime execution without URL-related errors.

---

## Preconditions

- User is logged in to the Elitea platform
- User has access to Credentials, Toolkits & Indexes, and Chat sections
- Valid GitHub credentials are available (Personal Access Token or GitHub App)
- Base URL: `https://api.github.com` or GitHub Enterprise URL

---

## Test Data

| Field | Value |
|-------|-------|
| Credential Display Name | autotest_github_trailing_slash |
| Credential ID | autotest-github-trailing-slash |
| Base URL | `https://api.github.com/` (with single trailing slash) |
| Auth Type | Bearer |
| API Token | Valid GitHub Personal Access Token |
| Toolkit Name | autotest_github_toolkit |

---

## Steps

### Part 1: Create Credential with trailing slash

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Credentials section | Credentials page loads successfully |
| 2 | Click "+ Credential" button | Credential type selection dialog opens |
| 3 | Select "GitHub" credential type | New GitHub Credential form opens |
| 4 | Enter Display Name: "autotest_github_trailing_slash" | Field accepts input |
| 5 | Enter ID: "autotest-github-trailing-slash" | Field accepts input |
| 6 | Enter Base URL WITH trailing slash: `https://api.github.com/` | Field accepts URL with trailing slash, slash remains visible |
| 7 | Select Auth type: "Bearer" | Bearer token field appears |
| 8 | Enter valid GitHub Personal Access Token | Field accepts input |
| 9 | Click "Test connection" button | Connection check initiates and succeeds (URL normalized server-side) |
| 10 | Click "Save" button | Success notification: "Credential saved successfully" |
| 11 | Verify credential appears in list | "autotest_github_trailing_slash" visible in credentials list with GitHub badge |

### Part 2: Create Toolkit

| # | Action | Expected Result |
|---|--------|-----------------|
| 12 | Navigate to Toolkits & Indexes section | Toolkits page loads successfully |
| 13 | Click "+ Toolkit" button | Toolkit type selection dialog opens |
| 14 | Select "GitHub" toolkit type | New GitHub Toolkit form opens |
| 15 | Enter Toolkit Name: "autotest_github_toolkit" | Field accepts input |
| 16 | In "GitHub Configuration" dropdown, select "autotest_github_trailing_slash" | Credential is selected, form shows credential details |
| 17 | Click "Save" button | Success notification: "Toolkit saved successfully" |
| 18 | Verify toolkit appears in list | "autotest_github_toolkit" visible in toolkits list |

### Part 3: Execute in Chat

| # | Action | Expected Result |
|---|--------|-----------------|
| 19 | Navigate to Chat section | Chat page loads successfully |
| 20 | Start a new chat conversation | New chat session opened |
| 21 | Attach "autotest_github_toolkit" to Chat | Toolkit attached, visible in Chat sidebar or attachments |
| 22 | Send message: "what can I do with the help of attached toolkit?" | AI responds with toolkit capabilities description |
| 23 | Send message requiring GitHub toolkit (e.g., "List my repositories") | Message sent, AI processes and invokes GitHub toolkit |
| 24 | Observe Chat response | Chat displays GitHub data (repositories list or appropriate response) |
| 25 | Verify no URL-related error messages | No errors about malformed URLs, double slashes, or trailing slashes |
| 26 | Send another GitHub query (e.g., "Get issues from repository X") | AI invokes GitHub toolkit again |
| 27 | Verify second execution succeeds | Chat displays GitHub issues data without errors |

---

## Expected Final State

- GitHub credential is saved with trailing slash visible in Base URL field
- Test Connection succeeds (URL normalized server-side)
- Toolkit successfully references the credential
- Chat executes GitHub toolkit without URL-related errors
- Multiple tool invocations work correctly in same chat session
- API endpoint construction is correct (no double slashes)

---

## Pass/Fail Criteria

**Pass:**
- Base URL field accepts trailing slash and keeps it visible in UI
- Test Connection succeeds with URL containing trailing slash
- Credential saves successfully
- Toolkit successfully links to credential
- GitHub toolkit invokes successfully from Chat
- Chat displays valid GitHub data
- Multiple GitHub tool calls succeed in same session
- No URL-related error messages appear
- API calls use correctly normalized URLs

**Fail:**
- Base URL field rejects or strips trailing slash in UI
- Test Connection fails due to trailing slash
- Credential fails to save
- Toolkit cannot reference credential
- GitHub toolkit invocation fails from Chat
- URL-related error messages appear
- Malformed URLs cause failures
- Chat displays errors instead of data

---

## Cleanup

- Delete Toolkit "autotest_github_toolkit"
- Delete Credential "autotest_github_trailing_slash"
