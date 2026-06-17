---
id: ELITEA-0258
title: "App Creation: Clear Error on Misconfigured Toolkit"
priority: high
type: functional
module: applications
status: draft
execution_type: manual
tags: [feat:toolkits, nfr:usability, eng:frontend, eng:backend, app:wikis, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770, EliteaAI/elitea_issues#4938]
---
# ELITEA-0258: App Creation: Clear Error on Misconfigured Toolkit

**Module:** Applications · **Priority:** High · **Type:** Functional

**Objective:** Verify that creating an app with a misconfigured toolkit shows a clear, specific, actionable error message — not a generic "Value error," popup.

**Coverage:**
- Selecting a toolkit with missing embedding model
- Error message is complete, specific, and actionable
- No generic truncated "Value error," popup shown

## Preconditions

- Logged in as a project member
- A toolkit with a configuration issue (missing embedding model) exists: GithubToolkitWithBroker
- Navigate to create a new DeepWiki application

## Test Data

Misconfigured toolkit: GithubToolkitWithBroker (missing embedding model reference)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the DeepWiki app creation form | Creation form is displayed |
| 2 | Fill in all mandatory fields; in the code toolkit dropdown select 'GithubToolkitWithBroker' | Toolkit is selected |
| 3 | Click the 'Save' button | An error message is displayed — the message is complete, identifies which field/toolkit has the issue, and provides actionable resolution guidance. It does NOT show a generic 'Value error,' truncated popup |

## Expected Final State

An error message is displayed — the message is complete, identifies which field/toolkit has the issue, and provides actionable resolution guidance. It does NOT show a generic 'Value error,' truncated popup

## Pass/Fail Criteria

**Pass:**
- Clear, complete error message displayed with field identification and resolution guidance

**Fail:**
- Generic 'Value error,' popup shown, or message is truncated/ends with comma and space
