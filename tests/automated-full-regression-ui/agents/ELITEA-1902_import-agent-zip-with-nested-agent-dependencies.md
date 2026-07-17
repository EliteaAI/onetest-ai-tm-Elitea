---
id: ELITEA-1902
title: "Import agent .zip with nested agent dependencies"
priority: high
type: functional
module: agents
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:agents]
requirements: []
automation_test_id: tests.ui.agents.test_import_agent_zip_nested_agent_dependencies.TestImportAgentZipNestedAgentDependencies.test_import_agent_zip_nested_agent_dependencies
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/606
---

# ELITEA-1902: Import agent .zip with nested agent dependencies

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that importing a .zip archive containing a main agent with nested agent dependencies creates all entities correctly and links them as expected.

---

## Preconditions

- User is logged in to the Elitea platform.
- An agent with nested agent dependencies has been exported as a .zip file (available for import).

---

## Test Data

| Field | Value |
|-------|-------|
| Import file | .zip archive produced by exporting an agent with nested agent dependencies |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Export an agent that has nested agent dependencies (produces a .zip) | A .zip file is downloaded containing the main agent and nested agents |
| 2 | Navigate to Agents → Import and upload the .zip file | The .zip file is uploaded and processed |
| 3 | Verify the import wizard lists entity cards for the main agent AND all nested dependencies | Entity cards for the main agent and all nested agents are shown |
| 4 | Confirm the import | The import operation completes |
| 5 | Verify the main agent and all nested agents are created in the project | All entities appear in the Agents dashboard |
| 6 | Open the main agent — verify nested agents are correctly linked | The main agent's configuration shows the nested agents as attached dependencies |

---

## Expected Final State

The main agent and all its nested agent dependencies are created in the project, and the main agent correctly links to all nested agents.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All entities are created and the main agent correctly links to its nested agent dependencies.

**Fail:**
- Any step produces an error or unexpected result.
- The import fails, some entities are not created, or nested agents are not linked to the main agent.
