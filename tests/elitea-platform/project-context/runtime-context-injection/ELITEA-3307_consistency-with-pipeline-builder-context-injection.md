---
id: ELITEA-3307
title: "Skill Builder behaves consistently with Pipeline Builder regarding context injection"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, pipeline-builder, skills-builder, consistency]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3307: Skill Builder behaves consistently with Pipeline Builder regarding context injection

## Preconditions

- User is logged in to `{{base_url}}`
- Agent & Pipeline Builder module is enabled
- Skills Builder module is enabled
- User is in a test project

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Agent & Pipeline Builder and Skills Builder in Chat Modules | Both modules are enabled |
| 2 | Send: "Create a pipeline called 'Data Processor' that takes input and processes it through an LLM" | Pipeline is created in the current project without asking for project specification |
| 3 | Note the behavior: was project_id asked? Was the pipeline created in the current project? | Pipeline created in current project, no project_id question |
| 4 | Send: "Create a skill called 'Code Reviewer' that reviews code for best practices" | Skill is created |
| 5 | Verify Skill Builder behavior matches Pipeline Builder | Skill created in current project without asking for project specification |
| 6 | Compare both creation flows | Both tools receive context automatically and behave identically regarding project targeting |

## Expected Final State

Skill Builder and Pipeline Builder exhibit identical behavior regarding automatic context injection. Both tools create entities in the current project without requiring manual project specification.

## Pass/Fail Criteria

**Pass:**
- Both Pipeline Builder and Skill Builder create entities in current project automatically
- Neither tool asks for project_id during creation
- Behavior is consistent between the two tools

**Fail:**
- Skill Builder asks for project_id while Pipeline Builder doesn't (or vice versa)
- One tool creates in current project while the other requires specification
- Inconsistent user experience between the tools
