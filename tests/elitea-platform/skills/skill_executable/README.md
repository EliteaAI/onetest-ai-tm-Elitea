# Skill Executable - Test Suite

Test cases for **Story #6920: Skill Run Engine & Run API** (Epic #6896 - Make "Skills" a separate executable entity).

## Critical P0 Test Coverage (11 Test Cases)

### Core Execution
1. **ELITEA-4230** - Execute default version and return run_id
2. **ELITEA-4231** - Execute specific version
3. **ELITEA-4232** - Sync mode returns response successfully

### Attribution
4. **ELITEA-4233** - Usage attribution with entity_type='skill'
5. **ELITEA-4234** - Response meta contains skill_run object

### Critical Errors
6. **ELITEA-4235** - Empty/blank instructions returns 400
7. **ELITEA-4236** - Non-existent skill/version returns 404

### Configuration
8. **ELITEA-4237** - LLM settings precedence
9. **ELITEA-4238** - Project context injected by default

### Regression
10. **ELITEA-4239** - Agent-attached skills via load_skill unchanged
11. **ELITEA-4240** - ~skill invocation from agent unchanged

## API Endpoint

```
POST /elitea_core/skill_predict/prompt_lib/{project_id}/{skill_id}[/{version_id}]
```

## Requirements

- EliteaAI/elitea_issues#6920 (Story S1)
- EliteaAI/elitea_issues#6896 (Parent Epic)
- EliteaAI/elitea_issues#7198 (Child QA Task)

## Test Execution Notes

- All tests require authentication to {{base_url}}
- Project must have default model configured
- Skills must be saved versions (not unsaved drafts)
- Usage tracking verification requires database/API access
- Regression tests compare against pre-S1 behavior

## Related Test Suites

- `/tests/elitea-platform/skills/` - Other skill functionality tests
- `/tests/elitea-platform/agents/` - Agent-related tests
- `/tests/elitea-platform/usage-cost-tracking/` - Usage attribution tests
