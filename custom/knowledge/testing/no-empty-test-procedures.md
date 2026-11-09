---
bc-version: [all]
domain: testing
keywords: [empty-test, stub, placeholder, no-assertion, false-green, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: no empty or assertion-free [Test] procedures

## Description

A `[Test]` procedure with no statements, or with only `[GIVEN]`/`[WHEN]`/`[THEN]` comments, runs and passes. In the AL Test Tool and in CI it shows as green, so a placeholder looks like covered functionality. The same applies to a test that performs an action but never asserts anything: it only proves the action did not raise an error. KOLLAB does not commit empty or assertion-free tests.

## Best Practice

Every `[Test]` procedure ends its `[THEN]` block with at least one assertion (`Assert.*`, `asserterror` with an error assertion, or a verifying `TestPage` check). When "the action succeeds" is the claim, still assert a resulting state — the posted entry exists, the status changed, the field has the expected value. Write planned tests as a list in the Jira task or a comment at the codeunit level, not as empty `[Test]` procedures.

## Anti Pattern

A `[Test]` procedure whose body is empty or contains only comments, a test that calls a helper such as `CreateCustomer()` whose body is empty, or a test whose `[THEN]` comment is followed by no assertion.
