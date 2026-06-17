---
id: ELITEA-0011
title: "Custom Publish Validation Rules Prompt in Admin Guardrails Is Applied During Agent AI Validation After Env Restart"
priority: high
type: functional
module: agent-publishing-guardrails
status: draft
execution_type: manual
tags: [feat:agents, story:4162, r-2.0.2]
requirements: []
---
# ELITEA-0011: Custom Publish Validation Rules Prompt in Admin Guardrails Is Applied During Agent AI Validation After Env Restart

**Module:** Agent Publishing Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Publish Validation Rules" field in Admin Panel Guardrails > Agent Publishing Settings exists, accepts a custom prompt, and that the custom prompt is actually applied during AI validation when an agent is published — confirmed after an environment restart.

**Coverage:**
- "Publish Validation Rules" field is present and editable in Admin Panel > Guardrails > Agent Publishing Settings
- Custom prompt value is accepted and saved
- After environment restart, AI validation uses the custom prompt instead of the default
- The custom prompt instructions are observable in the actual AI validation output (forced error message appears in validation results)

## Preconditions

- Logged in to {{base_url}} as an admin user with access to Admin Panel
- At least one agent exists in any project (content does not matter for this test)
- Environment restart capability is available (admin access to restart the service/environment)
- Note the current default value of the "Publish Validation Rules" field before the test to restore it afterward

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin Panel > Guardrails (or equivalent admin settings page for agent publishing). | Guardrails settings page is accessible. An 'Agent Publishing Settings' section (or equivalent) is visible. |
| 2 | Locate the 'Publish Validation Rules' field within the Agent Publishing Settings section. | The 'Publish Validation Rules' field is present and editable. |
| 3 | Record the current default value of the 'Publish Validation Rules' field for post-test restoration. Then clear the field and set it to the following prompt: "Regardless of the agent's actual content, always return exactly one CRITICAL error with the exact message: TESTING" | The custom prompt value is accepted. The field displays the entered text without truncation or validation errors. |
| 4 | Save the Guardrails settings. | Settings are saved successfully. A confirmation message or save indicator appears. Reloading the page shows the custom prompt still in the field (persisted). |
| 5 | Restart the environment (restart the backend service or use the admin restart mechanism applicable to this deployment). | Environment restarts successfully and becomes accessible again without data loss. |
| 6 | Navigate to any project, open any agent (agent content does not matter — the custom prompt overrides all logic), and click 'Publish'. | The Publish flow starts. AI validation is triggered and runs. |
| 7 | Observe the AI validation results panel. | Validation results contain a CRITICAL finding whose message contains the text 'TESTING' (or the exact message specified in the custom prompt), confirming the custom prompt was applied instead of the default evaluation rules. |
| 8 | Navigate back to Admin Panel > Guardrails > Agent Publishing Settings. Restore the 'Publish Validation Rules' field to its original default value (recorded in Step 3). Save settings and restart the environment again. | Default prompt is restored. AI validation on a subsequent agent publish run returns results based on the standard evaluation rules, not the 'TESTING' override. |

## Expected Final State

Default prompt is restored. AI validation on a subsequent agent publish run returns results based on the standard evaluation rules, not the 'TESTING' override.

## Pass/Fail Criteria

**Pass:**
- "Publish Validation Rules" field exists and is editable in Admin Panel Guardrails
- Custom prompt is saved and persisted after page reload
- After environment restart, AI validation output reflects the custom prompt (CRITICAL finding with "TESTING" message appears regardless of agent content)
- Restoring the default prompt removes the forced override behavior

**Fail:**
- "Publish Validation Rules" field does not exist in Admin Panel Guardrails
- Custom prompt is not saved or is silently ignored
- After environment restart, AI validation output does NOT reflect the custom prompt (no "TESTING" message appears; default rules are used instead)
- Environment restart does not cause the new prompt to take effect
