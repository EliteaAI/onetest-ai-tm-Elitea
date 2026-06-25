---
id: ELITEA-1701
title: "UI No Longer Shows Reload-Required Indicators for Live-Reload Settings"
priority: high
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1701: UI No Longer Shows Reload-Required Indicators for Live-Reload Settings

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Reload required" badges, post-save banners, and bottom bar indicators are removed for Blocked Toolkits, Blocked Tools, and Sensitive Action Tools settings after implementing live-reload behavior.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- Guardrails configuration page accessible

## Test Data

| Setting | Previous Behavior | Expected New Behavior |
|---------|------------------|----------------------|
| Blocked Toolkits | "Reload required" badge shown | No badge |
| Blocked Tools | "Reload required" badge shown | No badge |
| Sensitive Action Tools | "Reload required" badge shown | No badge |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Inspect the "Blocked Toolkits" field/section. | **No "Reload required" badge** is displayed next to this setting. |
| 3 | Inspect the "Blocked Tools" field/section. | **No "Reload required" badge** is displayed. |
| 4 | Inspect the "Sensitive Action Tools" field/section. | **No "Reload required" badge** is displayed. |
| 5 | Make a change to Blocked Toolkits (add or remove a toolkit). | Change is reflected in UI. |
| 6 | Click "Save Configuration". | Success notification shown. |
| 7 | Observe the post-save banner area. | **No yellow banner** mentioning pylon reload for these settings. |
| 8 | Observe the bottom bar / status bar. | **No "Reload required" indicator** referencing these settings. |
| 9 | Make changes to Blocked Tools and Sensitive Action Tools. Save. | Same behavior: no reload-required indicators. |
| 10 | Verify that other settings that DO require reload still show appropriate indicators. | Settings that legitimately need reload still show badges/banners. |

## Expected Final State

All "Reload required" indicators are removed specifically for Blocked Toolkits, Blocked Tools, and Sensitive Action Tools. Other settings that still require reload continue to show appropriate indicators.

## Pass/Fail Criteria

**Pass:**
- No "Reload required" badge on Blocked Toolkits field
- No "Reload required" badge on Blocked Tools field
- No "Reload required" badge on Sensitive Action Tools field
- Post-save banner does not mention these settings need reload
- Bottom bar does not show reload indicator for these settings
- Other reload-requiring settings still display indicators correctly

**Fail:**
- "Reload required" badge still appears on any of the three settings
- Post-save banner still lists these settings as requiring reload
- Bottom bar still shows reload indicator after saving these settings
- Indicator removal inadvertently affects other settings that need reload
