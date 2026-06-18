---
id: ELITEA-0017
title: "Guardrail Settings Persistence Across Sessions"
priority: high
type: functional
module: agent-publishing-guardrails
status: ready
execution_type: manual
tags: [feat:agent-publishing, persistence, guardrails, story:4434, r-2.0.2, admin, p1]
requirements: [EliteaAI/elitea_issues#4434]
---
# ELITEA-0017: Guardrail Settings Persistence Across Sessions

**Module:** Agent Publishing Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that guardrail configuration (toggle state and exception projects) persists across page refreshes, browser sessions, and admin logout/login cycles.

## Preconditions

Admin access to configure guardrail
At least 2 projects for exception selection
elitea_core plugin can be reloaded

## Test Data

Toggle state: ON
Exception projects: Project Alpha, Project Beta

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin → Configuration → Guardrails | Guardrails page loads |
| 2 | Enable "Block Agent Publishing" toggle (ON) | Toggle switches to ON |
| 3 | Select "Project Alpha" and "Project Beta" as exception projects | Both projects selected |
| 4 | Click "Save" | Settings saved |
| 5 | Reload the elitea_core plugin | Plugin reloads successfully |
| 6 | Refresh the browser page (F5 or Ctrl+R) | Guardrails page reloads |
| 7 | Check "Block Agent Publishing" toggle state | Toggle is still ON |
| 8 | Check exception projects dropdown | "Project Alpha" and "Project Beta" are still selected |
| 9 | Navigate away to another Admin page (e.g., Users) | Users page loads |
| 10 | Navigate back to Configuration → Guardrails | Guardrails page loads again |
| 11 | Verify toggle state and exception projects persist | Toggle ON, exception projects still selected |
| 12 | Log out from Admin portal | Logout successful |
| 13 | Log back in with the same admin credentials | Login successful, Admin portal loads |
| 14 | Navigate to Configuration → Guardrails | Guardrails page loads |
| 15 | Verify toggle state and exception projects persist after logout/login | Toggle ON, exception projects still selected |
| 16 | Verify guardrail is still enforced (check Publish button in non-exception project) | "Publish" is disabled in non-exception projects |

## Expected Final State

"Publish" is disabled in non-exception projects

## Pass/Fail Criteria

PASS:
- Toggle state persists across page refresh
- Exception projects selection persists across page refresh
- Settings persist across navigation within Admin portal
- Settings persist across admin logout and login
- Guardrail enforcement continues to work correctly after all persistence tests

FAIL:
- Toggle state resets to OFF after page refresh
- Exception projects are cleared after page refresh
- Settings are lost when navigating to other Admin pages
- Settings reset after logout/login
- Guardrail stops being enforced despite persisted settings
