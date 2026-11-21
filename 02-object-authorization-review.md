# Lab 2 — Object-level authorization review

**Status:** Fictional, local-only demonstration scenario  
**Objective:** Verify that a signed-in training user can access only records they are allowed to see.  
**Authorized scope:** A mock records application and two disposable fixture users on `localhost`.  
**Data handling:** All names and records are fictional; no real identifiers or accounts are used.

## Goal

Assess whether the server checks record ownership for every read and update, rather than trusting an identifier supplied by the browser.

## Reproduction outline

1. Create two disposable users and one sample record for each in the local fixture.
2. Sign in as the first user and view that user's own record.
3. In the fixture only, request the second sample record using the first user's session.
4. Repeat with an update attempt and confirm the server rejects access without changing the second record.
5. Preserve only sanitized status codes and fixture output; never test this pattern on a real service without written authorization.

## Demonstration observation

The fictional vulnerable fixture returns another user's sample record when its identifier is changed. The expected secure behavior is a denial or a not-found response, with no data disclosed or modified.

## Impact

If an application relies on unguessable identifiers without checking authorization, users may access or alter other users' information. Identifier complexity is not an authorization control.

## Recommended remediation

- Enforce authorization on the server for every record read, update, and delete.
- Scope database queries to the authenticated user's permitted records.
- Add regression tests for cross-user access attempts.
- Log denied access safely without recording sensitive values.
- Re-run the same fixture checks after the fix and verify that no record changed.

## Evidence to add when performing a real lab

- Sanitized request/response pair showing the expected denial.
- Regression-test output for both read and update attempts.
- A brief confirmation that the second fixture record remained unchanged.

## Lesson

Authentication tells the application who is signed in; authorization determines which specific records that identity may access.
