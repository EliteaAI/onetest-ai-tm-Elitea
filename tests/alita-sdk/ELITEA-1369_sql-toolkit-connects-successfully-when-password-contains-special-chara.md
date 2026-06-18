---
id: ELITEA-1369
title: "SQL Toolkit Connects Successfully When Password Contains Special Characters (e.g., `@`)"
priority: high
type: functional
module: alita-sdk
status: ready
execution_type: manual
tags: [feat:toolkits, r-2.0.3]
requirements: []
---
# ELITEA-1369: SQL Toolkit Connects Successfully When Password Contains Special Characters (e.g., `@`)

**Module:** Alita Sdk · **Priority:** High · **Type:** Functional

**Objective:** Verify that a SQL Toolkit successfully connects to a database when the password contains special characters — specifically the `@` symbol — without the connection string being misinterpreted.

**Root Cause Context (bug #2601):** The connection string parser splits on the `@` character to separate credentials from the host. A password containing `@` (e.g., `password@123`) causes the string to be split at the wrong position, resulting in a malformed host/credentials and a connection error.

**Coverage:**
- SQL Toolkit configured with a password containing `@` connects successfully
- SQL Toolkit configured with a password containing other special characters (`#`, `$`, `!`, `%`) also connects successfully
- Connection string is not exposed in error messages or logs

## Preconditions

- A SQL database instance is accessible (e.g., PostgreSQL or MySQL)
- The database has a user whose password contains the `@` symbol (e.g., `pass@word1`)
- The user has permission to create/edit Toolkits in the project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits and create a new SQL Toolkit (or open an existing one) | SQL Toolkit configuration form is open |
| 2 | Fill in the connection details: host, port, database name, username, and set the password to a value containing `@` (e.g., `pass@word1`) | All fields are filled; connection string is constructed internally by the application |
| 3 | Save the Toolkit configuration | Toolkit is saved without validation errors |
| 4 | Open the Toolkit Test Settings panel and run a simple test query (e.g., list tables or `SELECT 1`) | Connection is established successfully; a valid query result is returned — no connection error or string parsing error |
| 5 | Repeat steps 1–4 with password variants containing other special characters: `#`, `$`, `!`, `%` (one at a time) | Each password variant connects successfully — no character causes a misinterpretation or connection failure |

## Expected Final State

Each password variant connects successfully — no character causes a misinterpretation or connection failure

## Pass/Fail Criteria

PASS: Connection succeeds and toolkit test returns a valid result for passwords with `@`, `#`, `$`, `!`, `%`
FAIL: Connection error is shown; string is misinterpreted; host or credentials are incorrectly parsed
