---
id: ELITEA-1774
title: "SharePoint Personal URL — Site URL Format Accepted in Configuration"
priority: critical
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [integration:sharepoint, feat:toolkits, personal-urls, configuration, r-2.0.4]
requirements: [EliteaAI/elitea_issues#3054]
---
# ELITEA-1774: SharePoint Personal URL — Site URL Format Accepted in Configuration

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that personal SharePoint site URL formats (e.g., `https://company-my.sharepoint.com/personal/user/`) are accepted in the Site URL configuration field without validation errors.

## Preconditions

- User has access to {{base_url}}
- User knows their personal SharePoint URL structure

## Test Data

- Personal site URL format: `https://epam-my.sharepoint.com/personal/firstname_lastname/`
- Organizational site URL format (for comparison): `https://epam.sharepoint.com/sites/TeamSite/`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials → Click "+ Credential" | Credential creation form opens |
| 2 | Select "SharePoint" type | SharePoint configuration form displayed |
| 3 | Enter personal Site URL: `https://epam-my.sharepoint.com/personal/firstname_lastname/` | URL field populated |
| 4 | Tab out of Site URL field or click elsewhere | No validation error appears; Field accepts personal URL format |
| 5 | Complete other required fields (Client ID, Secret, Auth type) | Fields populated |
| 6 | Click "Save" or "Test connection" | Action proceeds without URL format rejection |
| 7 | Verify personal URL format persists after save | Configuration saved; Personal URL visible in Site URL field when reopened |

## Expected Final State

Personal SharePoint URL format accepted and saved in configuration

## Pass/Fail Criteria

**Pass:**
- Personal URL format (`company-my.sharepoint.com/personal/user/`) accepted
- No validation error: "Invalid URL format" or "Personal URLs not supported"
- URL saved correctly
- Test connection succeeds with personal URL

**Fail:**
- Validation error appears for personal URL format
- Field rejects `-my.sharepoint.com` domain
- URL not saved or modified after save
