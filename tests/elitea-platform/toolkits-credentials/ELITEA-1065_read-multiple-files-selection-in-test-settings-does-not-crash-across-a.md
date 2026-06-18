---
id: ELITEA-1065
title: "Read multiple files selection in Test Settings does not crash across all affected toolkits"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5002]
---
# ELITEA-1065: Read multiple files selection in Test Settings does not crash across all affected toolkits

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting "Read multiple files" from the Test Settings tool dropdown in each previously affected toolkit type (Artifact, GitHub, GitLab, Bitbucket) no longer triggers a `ReferenceError: Tooltip is not defined` crash.

**Coverage:**
- No crash or error overlay on selecting Read multiple files in Artifact toolkit Test Settings
- No crash in GitHub toolkit Test Settings
- No crash in GitLab toolkit Test Settings
- No crash in Bitbucket toolkit Test Settings
- All required form fields (File Paths*, Bucket Name, Offset, Limit, Skip Size Check) are rendered after selection

## Preconditions

- Logged into {{base_url}} with a Private project account
- At least one each of Artifact, GitHub, GitLab, Bitbucket toolkits configured with "Read multiple files" tool enabled

## Test Data

- Artifact toolkit: any configured Artifact toolkit (e.g. "Artifact regression", bucket: regr)
- GitHub toolkit: any configured GitHub toolkit with "Read multiple files" enabled
- GitLab toolkit: any configured GitLab toolkit with "Read multiple files" enabled
- Bitbucket toolkit: any configured Bitbucket toolkit with "Read multiple files" enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits and open an Artifact toolkit that has 'Read multiple files' enabled. | Toolkit detail page opens on the Configuration tab with the Test Settings panel visible on the right. |
| 2 | In the Test Settings panel, click the Tool dropdown and select 'Read multiple files'. | Page does NOT crash. Form renders with fields: File Paths* (array input), Bucket Name, Offset, Limit, Skip Size Check checkbox. RUN TOOL button is visible. |
| 3 | Open a GitHub toolkit and repeat: click the Tool dropdown in Test Settings and select 'Read multiple files'. | No crash. Required fields render correctly. |
| 4 | Open a GitLab toolkit and repeat the same selection. | No crash. Required fields render correctly. |
| 5 | Open a Bitbucket toolkit and repeat the same selection. | No crash. Required fields render correctly. |

## Expected Final State

No crash. Required fields render correctly.

## Pass/Fail Criteria

**Pass:**
- Selecting "Read multiple files" completes for all 4 toolkit types without any error overlay
- Required fields are visible and interactable after selection in every toolkit

**Fail:**
- Any toolkit shows a full-screen error overlay (Tooltip is not defined or any other JS crash) after selecting "Read multiple files"
- Fields fail to render after selection in any toolkit
