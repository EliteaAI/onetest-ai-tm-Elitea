---
id: ELITEA-3210
title: "Viewer Role and the Share Toggle on Own Personal Secrets — Record Actual Behavior (Open Question)"
priority: medium
type: security
module: secrets
status: draft
execution_type: manual
tags: [feat:secrets, story:5633, private-project-secrets, ui, viewer-role, open-question]
requirements: [EliteaAI/elitea_issues#5633]
---
# ELITEA-3210: Viewer Role and the Share Toggle on Own Personal Secrets — Open Question

**Module:** Secrets · **Priority:** Medium · **Type:** Security

**Objective:** Companion UI check to ELITEA-3206's code-node open question: does a Viewer-role user see and control the share toggle on their own personal secrets? Record actual behavior as a finding rather than assuming a contract.

**Note:** Pass/Fail is not applicable in the usual sense — record the result as a finding, same framing as ELITEA-3206.

## Preconditions

- A user with Viewer role on the relevant project, with their own personal project and at least one personal secret

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | As the Viewer-role user, open their own personal project's Secrets page. | Record whether the page/section is accessible at all. |
| 2 | If accessible, locate the share toggle on one of their own secrets. | Record whether it's visible, and if visible, whether it's interactive or disabled. |
| 3 | If interactive, attempt to flip it. | Record whether the change succeeds. |

## Finding template

- Secrets page accessible to Viewer for own personal project: `<yes / no>`
- Toggle visible: `<yes / no>`
- Toggle interactive: `<yes / no / n/a>`
- Toggle change succeeds: `<yes / no / n/a>`
- Consistent with ELITEA-3206's code-node finding: `<yes / no>`
- Recommended follow-up: `<none / raise as UX question / raise as bug>`
