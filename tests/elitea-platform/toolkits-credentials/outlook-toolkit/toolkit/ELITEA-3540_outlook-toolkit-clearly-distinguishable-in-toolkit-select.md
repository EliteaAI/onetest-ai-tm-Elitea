---
id: ELITEA-3540
title: "Outlook Toolkit Clearly Distinguishable in Toolkit Selection List"
priority: medium
type: functional
module: outlook-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.7, eng:sdk, int:oauth, nfr:documentation]
requirements: [EliteaAI/elitea_issues#6784]
---
# ELITEA-3540: Outlook Toolkit Clearly Distinguishable in Toolkit Selection List

**Module:** Outlook Toolkit · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the Outlook toolkit is visually distinguishable (icon, name) in the toolkit selection list used by Agents/Pipelines when choosing which toolkits to attach.

## Preconditions

- At least one Outlook toolkit and one non-Outlook toolkit exist in the project

## Test Data

- N/A (UI inspection only)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the toolkit selection list on an Agent or Pipeline configuration screen | List of available toolkits is shown |
| 2 | Locate the Outlook toolkit entry | It shows a distinct Outlook icon and its configured name, clearly distinguishable from SharePoint/other toolkits in the same list |

## Expected Final State

The Outlook toolkit is unambiguously identifiable in the selection list.

## Pass/Fail Criteria

**Pass:**
- Outlook toolkit has a distinct icon/label in the selection list

**Fail:**
- Outlook toolkit is unlabeled, mislabeled, or shares an icon with an unrelated toolkit type
