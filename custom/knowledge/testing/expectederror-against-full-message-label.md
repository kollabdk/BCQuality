---
bc-version: [all]
domain: testing
keywords: [asserterror, expectederror, label, error-message, negative-test, substring, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: assert expected errors against the full message in a Label

## Description

KOLLAB policy. It extends `microsoft/knowledge/testing/asserterror-needs-expectederror-and-code.md`. `Assert.ExpectedError` passes when the last error text contains the expected text, so a short literal such as `'Open'` or `'Status'` matches almost any error from the same area — a missing setup or a status error from a different check makes the test green without exercising the rule it claims to test. KOLLAB negative tests therefore assert against the complete error message, held in a Label in the test codeunit.

## Best Practice

Declare a Label in the test codeunit with the same text as the error Label in the app, including its placeholders, and build the expected message with `StrSubstNo` and the values from the test. Pass that to `Assert.ExpectedError` directly after the `asserterror` statement. For `TestField` errors, use the dedicated assertion (`Assert.ExpectedTestFieldError`) instead of matching text. Name the Label after the error it represents (`CannotShipWithoutCertificateErr`).

## Anti Pattern

`Assert.ExpectedError('Open')` or another one- or two-word literal substring, an expected message typed inline as a literal instead of a Label, or a message that drops the field values the real error contains.
