# Lab 3 — Input validation and safe query handling

**Status:** Fictional, local-only demonstration scenario  
**Objective:** Review how a training search form handles unexpected input and whether data stays separate from query instructions.  
**Authorized scope:** A mock application with a disposable local database and synthetic records.  
**Data handling:** No production data, secrets, or third-party targets are involved.

## Goal

Confirm that the server validates input and uses parameterized database operations rather than building executable queries from raw user input.

## Reproduction outline

1. Review the local fixture's search handler and identify where input reaches the database layer.
2. Submit ordinary values, empty values, and boundary-length values through the training form.
3. Use the lab's benign test cases to check that input is treated as data and that validation errors are handled safely.
4. Confirm that malformed input does not expose stack traces or alter unrelated fixture records.
5. Do not use destructive payloads or try these checks against systems outside the explicitly authorized lab.

## Demonstration observation

The fictional vulnerable fixture concatenates a search value into a query. The secure expected behavior is a parameterized query, server-side validation, and a generic safe error for invalid input.

## Impact

Unsafe query construction can allow input to change query behavior. Poor error handling can also reveal implementation details. The actual risk depends on the database permissions, data sensitivity, and surrounding controls.

## Recommended remediation

- Use parameterized queries or a safe data-access layer.
- Validate type, length, and allowed format on the server.
- Give the application's database account only the permissions it needs.
- Return safe validation messages and keep diagnostic detail in protected logs.
- Add tests for ordinary, boundary, and malformed inputs, then verify stored fixture data is unchanged.

## Evidence to add when performing a real lab

- Sanitized test matrix and response status/results.
- Relevant safe code diff or configuration snippet.
- Regression-test output confirming input remains data.

## Lesson

Input validation improves correctness, while parameterization provides the key separation between user-supplied data and query structure.
