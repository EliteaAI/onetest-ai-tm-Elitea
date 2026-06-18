---
id: ELITEA-1368
title: "SQL Toolkit — execute_sql and list_tables_and_columns Run Successfully With Valid Credentials"
priority: critical
type: functional
module: alita-sdk
status: ready
execution_type: manual
tags: [feat:toolkits, int:sql, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4972]
---
# ELITEA-1368: SQL Toolkit — execute_sql and list_tables_and_columns Run Successfully With Valid Credentials

**Module:** Alita Sdk · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the SQL Toolkit tools `execute_sql` and `list_tables_and_columns` execute successfully without errors when valid database credentials are configured — no internal exceptions or logger-related failures.

**Coverage:**
- `execute_sql` runs a simple query and returns expected results
- `list_tables_and_columns` returns the database schema without error
- No `cannot access local variable 'logger'` or similar internal exception is thrown

## Preconditions

- Logged in to {{base_url}}
- A SQL Toolkit is configured with valid credentials for a PostgreSQL database (e.g., NeonDB)
- The configured database user has SELECT permissions

## Test Data

- Database type: PostgreSQL (e.g., NeonDB)
- Test query for execute_sql: `SELECT 1` or `SELECT * FROM <table_name> LIMIT 1`
- Valid credentials: host, port, database name, username, password

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Toolkit Test Settings panel. Select the `list_tables_and_columns` tool and run it. | Tool executes successfully. A list of tables and columns from the database is returned. No error message appears. |
| 2 | Select the `execute_sql` tool. Enter a simple query (e.g., `SELECT 1` or `SELECT * FROM <any_table> LIMIT 1`) and run it. | Tool executes successfully. Query results are returned. No `cannot access local variable 'logger'` error or any other internal exception appears. |

## Expected Final State

Tool executes successfully. Query results are returned. No `cannot access local variable 'logger'` error or any other internal exception appears.

## Pass/Fail Criteria

**Pass:**
- `execute_sql` returns valid query results without any error
- `list_tables_and_columns` returns the database schema without any error

**Fail:**
- Either tool returns `cannot access local variable 'logger'` or any other internal exception
- Tool execution fails despite valid credentials
