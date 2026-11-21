# Lab 1 — Session cookie security review

**Status:** Fictional, local-only demonstration scenario  
**Objective:** Review whether a training application's session cookie is configured to reduce exposure.  
**Authorized scope:** A mock application bound to `localhost`; no external system.  
**Data handling:** No real credentials or session tokens are included.

## Goal

Check the application's session-cookie attributes and explain why secure defaults matter.

## Reproduction outline

1. Sign in using the training fixture's disposable test account.
2. Inspect the response headers in the local browser's developer tools.
3. Record whether the session cookie uses `HttpOnly`, `Secure` when served over HTTPS, and an appropriate `SameSite` policy.
4. Sign out and confirm the session is invalidated; do not copy the cookie value into notes or screenshots.

## Demonstration observation

In this fictional example, the cookie is missing `HttpOnly` and has no explicit `SameSite` value. This is an expected sample observation, not a claim about a real application.

## Impact

Without `HttpOnly`, client-side script may be able to read the cookie if a script-injection flaw exists. A missing `SameSite` policy can increase cross-site request risk depending on the application's other protections. These flags do not replace output encoding, CSRF defenses, or secure session handling.

## Recommended remediation

- Set `HttpOnly` on session cookies.
- Set `Secure` in HTTPS environments.
- Choose `SameSite=Lax` or a stricter policy where the login flow permits it.
- Rotate and invalidate sessions on sign-out and sensitive account changes.
- Recheck response headers and authentication behavior after the change.

## Evidence to add when performing a real lab

- Sanitized header screenshot with cookie values fully hidden.
- Before/after configuration or test output.
- A short note confirming sign-out invalidation.

## Lesson

Cookie flags reduce specific session risks, but they need to be combined with sound authentication, authorization, and output-safety controls.
