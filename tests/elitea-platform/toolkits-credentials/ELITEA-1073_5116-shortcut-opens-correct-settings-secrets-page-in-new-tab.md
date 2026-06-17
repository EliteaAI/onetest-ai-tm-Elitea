---
id: ELITEA-1073
title: "[#5116] Shortcut Opens Correct Settings → Secrets Page in New Tab"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:credentials, feat:settings, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-1073: [#5116] Shortcut Opens Correct Settings → Secrets Page in New Tab

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking "New Private/Project Secret" opens the correct Settings → Secrets page in a new browser tab with `?createSecret=1` in the URL and the creation form already active.

**Test Data (Parametrized):**

| # | Project Type | Button Clicked | Expected Target |
|---|---|---|---|
| A | Private | "New Private Secret" | Private project Settings → Secrets |
| B | Team | "New Project Secret" | Team project Settings → Secrets |

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has secret create/list permissions
- A credential creation form is open with a token field in Secret mode and the secret dropdown open (per TC-NEW-01 setup)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the secret dropdown on a credential token field in Secret mode (per steps 1–5 from the preceding TC). | Secret dropdown is open showing CREATE and SAVED SECRETS sections. |
| 2 | Note the currently open browser tabs. | Baseline tab count noted. |
| 3 | Click 'New Private Secret' (row A) or 'New Project Secret' (row B) from the CREATE section. | A new browser tab opens. The original credential form tab remains open and unchanged. |
| 4 | Switch to the newly opened tab and inspect the URL. | URL contains `?createSecret=1` (e.g., `.../settings/secrets?createSecret=1`) and belongs to the correct project matching the parameter row. |
| 5 | Inspect the Settings → Secrets page content in the new tab. | The new secret creation input row/form is already active — the user does not need to click '+' manually. |
| 6 | Switch back to the original credential form tab. | The credential form still shows all previously entered data (Display Name, auth type, Secret mode selected). No data is lost. |

## Expected Final State

The credential form still shows all previously entered data (Display Name, auth type, Secret mode selected). No data is lost.

## Pass/Fail Criteria

**Pass:** New tab opens with correct URL including `?createSecret=1`; correct project targeted; creation form auto-triggered; credential form data preserved on return.
**Fail:** Same tab navigates away; wrong project URL opened; `?createSecret=1` absent from URL; creation form requires manual '+' click; credential form data lost.
