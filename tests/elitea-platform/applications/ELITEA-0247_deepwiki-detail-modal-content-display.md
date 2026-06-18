---
id: ELITEA-0247
title: "DeepWiki Detail Modal: Content Display"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, 4770]
requirements: [EliteaAI/elitea_issues#4770]
---
# ELITEA-0247: DeepWiki Detail Modal: Content Display

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the DeepWiki detail modal opens via the chip click and displays all required content correctly.

**Coverage:**
- Modal opens on Deepwiki chip click with background overlay
- Title, icon, primary description, use-case line, "What it includes" section, and three capability chips

## Preconditions

- Logged in as a project member
- On the Request App tab

## Test Data

Expected capability chips: 'Repository wiki generation', 'Architecture summaries', 'Code-aware Q&A'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the 'Deepwiki' chip on the DeepWiki card | Modal opens; background overlay is applied |
| 2 | Observe the modal title | 'DeepWiki' is displayed |
| 3 | Observe the modal icon | Placeholder/puzzle icon is shown |
| 4 | Observe the primary description | 'Generate searchable wiki pages from repository code and keep architecture context close to delivery work.' |
| 5 | Observe the use-case line | 'Teams that need onboarding material, implementation context, or durable knowledge for active repositories.' |
| 6 | Observe the 'What it includes' section header | Section header is visible |
| 7 | Observe the capability chips | 'Repository wiki generation', 'Architecture summaries', and 'Code-aware Q&A' are all shown |

## Expected Final State

'Repository wiki generation', 'Architecture summaries', and 'Code-aware Q&A' are all shown

## Pass/Fail Criteria

**Pass:**
- All modal content matches expected values exactly
- Modal opens with background overlay

**Fail:**
- Any field missing, wrong text, or modal does not open
