# Insecure File Upload Validation — Training Lab Write-up

**Category:** Web Application Security  
**Environment:** Authorized training lab (Hack The Box Academy)  
**Author:** Raad Raoof

## Summary

This exercise examined a web application's file-upload feature to understand how client-side controls, filename-extension checks, and MIME-type validation interact. The main lesson was that accepting an upload, storing a file, making it reachable, and executing it on the server are distinct outcomes that must be assessed separately.

## Objective

Evaluate the upload workflow and determine whether validation decisions were sufficiently enforced by the server. Testing was limited to the designated training environment.

## Methodology

1. Inspected the upload form to identify its request method, multipart encoding, input field, and any client-side restrictions.
2. Submitted a benign image and inspected the HTTP request and response using Burp Suite.
3. Compared client-side behavior with server-side responses to distinguish UI restrictions from server-enforced controls.
4. Reviewed the validation logic available within the lab to understand how filename extensions and MIME information were evaluated.
5. Considered the complete file lifecycle: acceptance, storage location, URL accessibility, and whether the server interpreted uploaded content as executable.

## Observations

The lab illustrated why extension checks and MIME-type checks must not be treated as sufficient proof that an upload is safe. Client-supplied content types can be manipulated, and extension filtering can be incomplete. A successful upload response alone does not demonstrate that the uploaded content is publicly accessible or executable.

## Security Impact

If an application accepts dangerous content and stores it in a location where the server interprets it as executable code, the issue may lead to unauthorized code execution. The actual impact depends on server configuration, storage location, permissions, and execution handling; it should not be assumed without evidence.

## Recommended Remediation

- Use a strict allowlist of permitted file types and verify file content using server-side inspection.
- Generate server-side filenames rather than trusting user-supplied names.
- Store uploads outside the web root where feasible, or serve them through a controlled download handler.
- Disable script execution in upload directories and apply least-privilege filesystem permissions.
- Enforce file-size limits and safely process or re-encode images when appropriate.
- Treat client-side validation as usability support only, never as the security boundary.
- Log rejected uploads and test validation against malformed and unexpected files.

## Learning Outcomes

- Distinguished client-side restrictions from server-side validation.
- Practiced inspecting multipart HTTP traffic with Burp Suite.
- Learned to assess upload acceptance, storage, reachability, and execution as separate stages.
- Connected observed behavior to practical remediation controls.

## Scope and Limitations

This is an educational lab write-up, not a report of a production vulnerability. No real users or third-party systems were tested. Target-specific paths, payloads, and challenge flags have intentionally been excluded.
