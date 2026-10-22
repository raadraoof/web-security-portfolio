# SQL Injection and Excessive Database Privileges — Training Lab Write-up

**Category:** Injection / Database Security  
**Environment:** Authorized training lab (Hack The Box Academy)  
**Author:** Raad Raoof

## Summary

This lab exercise examined how unsafe handling of search input can allow SQL query manipulation. It also illustrated how excessive database permissions can increase the impact of an injection flaw beyond unintended data access.

## Objective

Understand the root cause of SQL injection, observe how query behavior can reveal information about a database, and identify the controls that prevent escalation from an application-layer flaw to broader server impact.

## Methodology

1. Intercepted application requests and identified a search input that influenced database-backed results.
2. Used controlled test inputs in the designated lab to determine whether the input was handled as data or could alter query logic.
3. Observed differences in application responses to understand the potential for unintended query behavior.
4. Reviewed the lab scenario's database permissions and application architecture to understand why privilege boundaries matter.
5. Documented the security implications and defensive controls without including target-specific extraction queries, credentials, flags, or command-execution payloads.

## Finding and Analysis

SQL injection occurs when untrusted input is incorporated into a SQL statement in a way that changes the statement's intended structure. If database permissions are broader than the application requires, a successful injection may have a larger impact, potentially including unauthorized data access or access to database features that should not be available to the application.

The severity of a real finding depends on the vulnerable query, database account permissions, database configuration, reachable data, and any additional security boundaries. A chain to operating-system command execution must not be assumed unless it is separately demonstrated and authorized.

## Recommended Remediation

- Use parameterized queries or prepared statements for all data values.
- Avoid constructing SQL statements through string concatenation with untrusted input.
- Apply least privilege to database accounts; grant only the permissions required for normal application operation.
- Separate application runtime accounts from administrative and maintenance accounts.
- Disable or restrict dangerous database capabilities that the application does not need.
- Return generic error messages to users while retaining useful, access-controlled diagnostic logs.
- Add regression tests for injection attempts and review data-access code during security testing.

## Learning Outcomes

- Practiced identifying and analyzing potentially injectable application inputs.
- Improved understanding of how database permissions affect exploitability and impact.
- Connected parameterized queries and least privilege to defense in depth.
- Learned to separate observed evidence from assumptions about possible escalation.

## Scope and Limitations

This is a sanitized educational write-up based on a controlled training lab. It is not a report of a production system or client engagement. Exploit strings, target details, account information, and challenge flags are intentionally excluded from this public-facing version.
