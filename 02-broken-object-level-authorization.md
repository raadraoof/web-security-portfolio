# Broken Object-Level Authorization (BOLA) — Training Lab Write-up

**Category:** API Security / Access Control  
**Environment:** Authorized training lab (Hack The Box Academy)  
**Author:** Raad Raoof

## Summary

This exercise explored a common API authorization weakness: an authenticated user can request an object by changing a user-controlled identifier, and the server fails to verify that the requested object belongs to, or is otherwise accessible by, that user.

## Objective

Assess whether object-level authorization was enforced for an API endpoint that returned business/report data. Testing was performed only in the provided training environment using a designated lab account.

## Methodology

1. Authenticated with the lab-provided account and inspected the API's documented endpoints.
2. Identified an endpoint that retrieved a report using an object identifier.
3. Established which organization or object was associated with the test account.
4. In the authorized lab, compared the endpoint's behavior when requesting an object outside the account's expected scope.
5. Evaluated whether the response exposed data associated with another object and recorded the result without retaining unnecessary sensitive data.

## Finding

The lab demonstrated that authentication and broad role permissions do not replace object-level authorization. An endpoint can accept a valid session and still disclose an object that the current user is not entitled to access if the server does not verify the relationship between the requester and the requested record.

## Potential Impact

Depending on the data returned and the reach of the endpoint, BOLA can expose records belonging to other users or organizations. The impact should be based on the sensitivity and scope of the accessible data; bulk access should not be attempted unless explicitly required and permitted by the lab rules.

## Recommended Remediation

- Enforce authorization checks on every object access, on the server side.
- Scope database queries to the authenticated user's tenant or ownership context instead of fetching records by identifier alone.
- Deny access when the requested object is outside the user's authorized scope; use consistent `403 Forbidden` or non-disclosing `404 Not Found` behavior as appropriate.
- Add automated tests for cross-user and cross-tenant access to every relevant endpoint.
- Log repeated denied object-access attempts and monitor for enumeration patterns.
- Do not rely on unpredictable identifiers as a substitute for authorization checks.

## Learning Outcomes

- Distinguished authentication, role-level authorization, and object-level authorization.
- Practiced reviewing API endpoints and response behavior.
- Learned why changing an identifier is a useful access-control test in an authorized environment.
- Identified server-side ownership checks and tenant-scoped queries as core mitigations.

## Scope and Limitations

This write-up describes an educational lab scenario and is not a claim of a real-world or client finding. Identifiers, account details, tokens, target URLs, and bulk-extraction scripts have been omitted.
