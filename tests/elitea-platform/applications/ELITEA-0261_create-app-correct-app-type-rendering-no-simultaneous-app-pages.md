---
id: ELITEA-0261
title: "Create App: Correct App Type Rendering — No Simultaneous App Pages"
priority: critical
type: functional
module: applications
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:apps, r-2.0.3, nfr:ui, 4770]
requirements: [EliteaAI/elitea_issues#4770, EliteaAI/elitea_issues#4908]
---
# ELITEA-0261: Create App: Correct App Type Rendering — No Simultaneous App Pages

**Module:** Applications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "Create App" from any entry point renders only the correct app creation form — not multiple forms simultaneously.

**Coverage:**
- DeepWiki card → only DeepWiki form, Inventory does NOT appear
- Inventory card → only Inventory form, DeepWiki does NOT appear
- DeepWiki modal → only DeepWiki form, not duplicated
- No simultaneous rendering of multiple app pages

## Preconditions

- Logged in as a project member
- On the Request App tab

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click '+ Create App' on the DeepWiki card | Creation page shows ONLY the DeepWiki form; Inventory page does NOT appear simultaneously |
| 2 | Navigate back to the Request App tab | Request App tab shown |
| 3 | Click '+ Create App' on the Inventory card | Creation page shows ONLY the Inventory form; DeepWiki page does NOT appear simultaneously |
| 4 | Navigate back; open the DeepWiki modal; click '+ Create App' inside the modal | Creation page shows ONLY the DeepWiki form; no other app type appears alongside it |
| 5 | Inspect the creation page for duplication | DeepWiki form is not duplicated on the page |

## Expected Final State

DeepWiki form is not duplicated on the page

## Pass/Fail Criteria

**Pass:**
- Each entry point opens exactly one app creation form of the correct type
- No simultaneous rendering of multiple app forms

**Fail:**
- Multiple app pages render simultaneously, or DeepWiki is duplicated on the creation page
