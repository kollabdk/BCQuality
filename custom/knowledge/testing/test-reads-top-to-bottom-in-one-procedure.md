---
bc-version: [all]
domain: testing
keywords: [readability, helper-procedures, inline, verify, arrange, subprocedures, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: a test reads top to bottom in its own procedure

## Description

KOLLAB policy. A reviewer should be able to read one `[Test]` procedure from top to bottom and see the whole scenario: what is set up, what action is taken, and what is checked. Generated tests tend to do the opposite — they extract each step into local helpers (`SetupScenario`, `PerformAction`, `VerifyResult`) for reuse, so the test body becomes a handful of calls and the reader has to jump between procedures to learn what is actually tested. KOLLAB prefers some repetition across tests over that indirection.

## Best Practice

Keep the `[WHEN]` action and every `[THEN]` assertion written out inline in the test procedure. Keep the `[GIVEN]` steps in the test too, one line per step; a call to a library procedure that creates one well-named record (`LibrarySales.CreateCustomer`, `LibraryThise.CreateItemWithLotTracking`) counts as one readable step and is fine — see `customer-test-library-codeunit.md`. Extract a local helper only when it creates a fixture, has a name that says exactly what it creates, and contains no assertions and no action under test. Repeating three or four similar lines in several tests is acceptable.

## Anti Pattern

A test body that consists only of calls such as `Initialize(); CreateScenario(...); RunScenario(...); VerifyScenario(...);`, local `Verify*` procedures that hold the assertions, a helper that both builds data and performs the action under test, or helpers that call other local helpers several levels deep. Each of these hides what the test checks behind a procedure name.
