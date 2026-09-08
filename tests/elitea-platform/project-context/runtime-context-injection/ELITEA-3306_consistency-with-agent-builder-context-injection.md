---
id: ELITEA-3306
title: "Project Context Builder behaves consistently with Agent Builder regarding context injection"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, agent-builder, project-context-builder, consistency]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3306: Project Context Builder behaves consistently with Agent Builder regarding context injection

## Preconditions

- User is logged in to `{{base_url}}`
- Agent & Pipeline Builder module is enabled
- Project Context Builder module is enabled
- User is in a test project

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Agent & Pipeline Builder and Project Context Builder in Chat Modules | Both modules are enabled |
| 2 | Send: "Create an agent called 'Test Agent' that answers questions about coding" | Agent is created in the current project without asking for project specification |
| 3 | Note the behavior: was project_id asked? Was the agent created in the current project? | Agent created in current project, no project_id question |
| 4 | Send: "Create project context describing this as a development environment for testing" | Project Context is created |
| 5 | Verify Project Context Builder behavior matches Agent Builder | Project Context created in current project without asking for project specification |
| 6 | Compare both creation flows | Both tools receive context automatically and behave identically regarding project targeting |

## Expected Final State

Project Context Builder and Agent Builder exhibit identical behavior regarding automatic context injection. Both tools create entities in the current project without requiring manual project specification.

## Pass/Fail Criteria

**Pass:**
- Both Agent Builder and Project Context Builder create entities in current project automatically
- Neither tool asks for project_id during creation
- Behavior is consistent between the two tools

**Fail:**
- Project Context Builder asks for project_id while Agent Builder doesn't (or vice versa)
- One tool creates in current project while the other requires specification
- Inconsistent user experience between the tools
