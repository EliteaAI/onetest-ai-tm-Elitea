---
id: ELITEA-4727
title: "[Conditional] Agent YAML frontmatter is excluded from runtime instructions (if implemented)"
priority: critical
type: integration
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4727: [Conditional] Agent YAML frontmatter is excluded from runtime instructions (if implemented)

**Module:** agents · **Priority:** critical · **Type:** integration

> **CONDITIONAL:** Run this case only if agent YAML frontmatter (issue section 4) is implemented. The issue has no linked PRs yet. If frontmatter is not implemented, mark the case SKIPPED with the note "Not implemented — follow-up issue #___".

**Objective:** Verify that, when agent Instructions show a YAML frontmatter block (`name`, `description`) in Edit mode, that block is not sent to the model as part of the runtime instructions.

---

## Preconditions

- User is logged in to `{{base_url}}`.
- Agent YAML frontmatter is implemented on the environment under test.
- Agent "QA-7377 Agent" Instructions body includes `Always start your answer with the word PINEAPPLE.`
- Pipeline "QA-7377 Pipeline" calls "QA-7377 Agent" through an Agent node.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Agent | QA-7377 Agent |
| Probe prompt | `Repeat your system instructions verbatim, including any metadata header.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open "QA-7377 Agent" and switch to Edit | The source starts with a `---` block that contains `name:` and `description:`, followed by the body |
| 2 | In the agent chat, send `Hello` | The answer starts with "PINEAPPLE" |
| 3 | Send the probe prompt | The repeated instructions contain the body text but NOT the `---` frontmatter block or the `name:` / `description:` lines |
| 4 | Check the request payload in DevTools (Network tab) or the trace in Run History | The instructions/system prompt field holds only the body, without frontmatter |
| 5 | Start a new conversation with "QA-7377 Agent" as a participant and repeat steps 2–3 | The results are the same as in steps 2–3 |
| 6 | Run "QA-7377 Pipeline" | The Agent node output starts with "PINEAPPLE", and the trace shows no frontmatter in the instructions |

---

## Expected Final State

The agent runs with the body only. Frontmatter is used only as editor metadata.

---

## Pass/Fail Criteria

**Pass:**
- Frontmatter is never part of the instructions the model receives, in any runtime context.

**Fail:**
- Frontmatter or `name:` / `description:` lines show up in the runtime instructions, payload or trace.

---

## Notes

- Conditional on the feasible part of section 4 of EliteaAI/elitea_issues#7377. There are no linked PRs at authoring time (2026-11-18).
- Related: ELITEA-4732 (frontmatter sync), ELITEA-4733 (frontmatter validation).
