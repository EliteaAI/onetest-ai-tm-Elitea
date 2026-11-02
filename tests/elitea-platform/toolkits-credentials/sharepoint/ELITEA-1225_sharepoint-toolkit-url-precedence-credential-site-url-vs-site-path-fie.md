---
id: ELITEA-1225
title: "SharePoint Toolkit — URL Precedence: Credential Site URL vs Site Path Field"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [feat:toolkits, feature:2584, r-2.0.4]
requirements: [EliteaAI/elitea_issues#2584]
---
# ELITEA-1225: SharePoint Toolkit — URL Precedence: Credential Site URL vs Site Path Field

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify the system resolves the target site URL deterministically based on the two authoritative sources — credential site_url and toolkit Site Path field. The tool-level path argument is a folder/document path scoped within the already-resolved site and does NOT override or compete with the credential URL or Site Path. Covers 3 scenarios: (A) tenant-only credential + Site Path → Site Path appended to tenant URL; (B) full-URL credential + empty Site Path → credential URL used as-is; (C) full-URL credential + non-empty Site Path → one of the two wins deterministically, no wrong-site access.

## Preconditions

- Logged in to ELITEA at {{base_url}}
- Credential A: Site URL https://your-tenant.sharepoint.com (tenant only)
- Credential B: Site URL https://your-tenant.sharepoint.com/sites/TestSite (full /sites/ URL)
- /teams/TestTeam and /sites/TestSite both accessible on the tenant
- A sub-folder Shared Documents/Reports exists in both sites

## Test Data

Scenario A: Credential=https://your-tenant.sharepoint.com | Site Path=teams/TestTeam | Tool folder arg=Shared Documents/Reports
Scenario B: Credential=https://your-tenant.sharepoint.com/sites/TestSite | Site Path=empty | Tool folder arg=Shared Documents/Reports
Scenario C: Credential=https://your-tenant.sharepoint.com/sites/TestSite | Site Path=teams/TestTeam | Tool folder arg=none

Note: In all scenarios, the tool-level path arg is a folder path WITHIN the resolved site — it does not override the site resolution.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure toolkit with Credential A and Site Path teams/TestTeam (Scenario A). Execute Get files list without a folder filter. | Files from .../teams/TestTeam are returned. The resolved site is the tenant URL + Site Path. No double-slash in metadata. |
| 2 | Now execute Get files list again with folder path Shared Documents/Reports as the tool-level argument. | Files from Shared Documents/Reports within .../teams/TestTeam are returned. The tool-level path scopes results within the already-resolved /teams/TestTeam site — it does not change which site is accessed. |
| 3 | Configure toolkit with Credential B and Site Path empty (Scenario B). Execute Get files list without a folder filter. | Files from .../sites/TestSite are returned. Credential URL is used as-is. |
| 4 | Execute Get files list with folder path Shared Documents/Reports as the tool-level argument. | Files from Shared Documents/Reports within .../sites/TestSite are returned. The resolved site remains .../sites/TestSite regardless of the tool-level path. |
| 5 | Configure toolkit with Credential B (full /sites/ URL) and Site Path teams/TestTeam (Scenario C). Execute Get files list. | Response is deterministic — tool accesses exactly one site (either Site Path overrides credential URL, or credential URL wins). No data from an unintended site. No silent fallback or mixed-site response. |
| 6 | Note which site was accessed in step 5. Verify behavior is consistent on repeated executions and matches any documented precedence rule (tooltip / release notes). | Same site is accessed on every run. Behavior is predictable and documentable. |

## Expected Final State

Same site is accessed on every run. Behavior is predictable and documentable.

## Pass/Fail Criteria

Pass:
- Scenario A: files returned from the site formed by tenant URL + Site Path; tool folder arg scopes within that site only
- Scenario B: files returned from the credential's full URL; tool folder arg scopes within that site only
- Scenario C: one site accessed deterministically on every run; no wrong-site data returned
- Tool-level path argument never changes which site is resolved — only which folder within the resolved site is queried
- No malformed URLs (double-slash, duplicated path segments) in any scenario

Fail:
- Tool-level path arg causes a different site to be accessed than what credential + Site Path resolved
- Any scenario returns data from an unintended site
- Scenario C produces a non-deterministic result (different site on different runs)
- Any HTTP 500 or unhandled exception
