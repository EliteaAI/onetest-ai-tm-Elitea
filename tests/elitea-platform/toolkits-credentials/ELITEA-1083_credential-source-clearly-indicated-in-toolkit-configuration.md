---
id: ELITEA-1083
title: "Credential source clearly indicated in toolkit configuration"
priority: high
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:toolkits, issue:4392, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4392]
---
# ELITEA-1083: Credential source clearly indicated in toolkit configuration

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the toolkit configuration UI clearly indicates the credential source (private vs project) so users understand which credentials are being used without ambiguity.

**Coverage:**
- Credential source is visually indicated in toolkit UI
- Users can distinguish between private and project credentials
- No ambiguity about which credentials are active
- Clear labeling or iconography for credential source

## Preconditions

- User is authenticated in ELITEA at {{base_url}}
- Team project with toolkit exists
- Both private and project-level credentials exist
- User has access to toolkit configuration
- Browser: Chrome/Edge latest

## Test Data

- Team project with multiple toolkits
- User with private credentials
- User without private credentials (for comparison)
- Both private and project-level credentials configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a toolkit configuration in a team project where private credentials are being used | Toolkit configuration page loads |
| 2 | Observe the credential dropdown or credential section in the UI | UI clearly indicates that private credentials are being used (e.g., label, badge, or icon) |
| 3 | Open another toolkit where project credentials are being used (user without private credentials) | Toolkit configuration page loads |
| 4 | Observe the credential dropdown or credential section in the UI | UI clearly indicates that project credentials are being used with visual distinction from private credentials |
| 5 | Verify consistency of credential source indication across different toolkit types | Credential source display is consistent across all toolkit types |

## Expected Final State

Credential source display is consistent across all toolkit types

## Pass/Fail Criteria

**Pass:**
- Toolkit UI clearly shows whether private or project credentials are in use
- Credential source is labeled or indicated with clear visual cues
- No ambiguity for users about credential source
- UI is consistent across toolkits

**Fail:**
- Credential source is not indicated in UI
- Users cannot tell if private or project credentials are being used
- Ambiguous or misleading credential information
- Inconsistent credential source display
