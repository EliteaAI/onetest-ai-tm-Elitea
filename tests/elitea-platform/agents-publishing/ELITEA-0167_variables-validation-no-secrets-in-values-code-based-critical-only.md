---
id: ELITEA-0167
title: "Variables Validation — No Secrets in Values (Code-Based, Critical Only)"
priority: high
type: functional
module: agents-publishing
status: ready
execution_type: manual
tags: [feat:agents, story:4049]
requirements: [ProjectAlita/projectalita.github.io#4049]
---
# ELITEA-0167: Variables Validation — No Secrets in Values (Code-Based, Critical Only)

**Module:** Agents Publishing · **Priority:** High · **Type:** Functional

**Objective:** Verify that code-based validation detects API keys and sensitive secret patterns in variable values and flags them as Critical. This is a deterministic pattern-matching check — no AI/LLM analysis.

**Coverage:**
- Variable value matching an API key pattern → Critical with attributed message
- Variable value matching a private key or token pattern → Critical with attributed message
- Variable with a normal, non-sensitive value → No issue
- Agent with no variables → Variables validation section skipped entirely

## Preconditions

Agent with configurable variables. Agent is not yet published.

**Test Data:**

| Variable Name | Default Value | Expected Section | Expected Finding |
|---------------|--------------|------------------|------------------|
| api_key | sk-abcdefghijklmnopqrstuv (API key pattern) | Critical issues | "Variable 'api_key' may contain a secret or API key" |
| db_password | ghp_token12312312312312345678 (token pattern) | Critical issues | "Variable 'db_password' may contain a secret or API key" |
| environment | production (normal value) | Absent | No issue raised |
| (no variables) | N/A | Absent | Variables section not shown at all |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure variables: api_key =  sk-abcdefghijklmnopqrstuv, db_password = ghp_token12312312312312345678, environment = production | All three variables saved |
| 2 | Click Publish → enter version name → accept agreement → click Publish | Validation runs; results panel shown |
| 3 | Check Critical issues section for api_key | api_key listed as Critical: "Variable 'api_key' may contain a secret or API key" |
| 4 | Check Critical issues section for db_password | db_password listed as Critical: "Variable 'db_password' may contain a secret or API key" |
| 5 | Check all sections for environment | environment absent from all sections (Critical, Warnings, Suggestions) |
| 6 | Remove all variables from the agent and save | Agent has no variables |
| 7 | Click Publish → enter version name → accept agreement → click Publish | Validation runs; results panel shown |
| 8 | Check for any Variables section in results | Variables section absent entirely from validation results |

## Expected Final State

Variables section absent entirely from validation results

## Pass/Fail Criteria

Pass: All secret-pattern rows produce Critical issues with correct message format; normal value absent from all sections; no-variable agent produces no Variables section.
Fail: Any secret-pattern row missing or wrong severity; normal value incorrectly flagged; Variables section shown for agent with no variables.
