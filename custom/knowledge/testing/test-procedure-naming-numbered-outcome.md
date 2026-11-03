---
bc-version: [all]
domain: testing
keywords: [naming, test-procedure, test-method, numbering, success, failure, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: name test procedures Test_NN_<Subject>_<Outcome>

## Description

KOLLAB policy, not a platform rule. Test procedures in KOLLAB test codeunits are named `Test_NN_<Subject>_<Outcome>`: a two-digit number, a PascalCase subject describing what is exercised, and `_Success` or `_Failure` stating whether the test expects the action to succeed or to raise an error. Examples: `Test_01_CreateSalesOrder_Success`, `Test_04_ShipmentWithCatchCertificate_Failure`. The number gives a stable execution and reading order in the AL Test Tool, and the outcome suffix lets a reader see the negative tests without opening them.

## Best Practice

Number tests within a codeunit without duplicates. Gaps are allowed and may be used to group related tests (01–09 for one sub-feature, 10–19 for the next). Use exactly `_Success` or `_Failure` — not `_Fail`, `_OK` or `_Error`. A `_Failure` test contains `asserterror` followed by an error assertion (see `expectederror-against-full-message-label.md`). Keep Jira keys out of the procedure name; put them in a `[SCENARIO]` comment if needed.

## Anti Pattern

Plain PascalCase names without number and outcome (`SalesOrderWithLot`), two procedures sharing the same number in one codeunit, a `_Failure` test that has no `asserterror`, a `_Success` test that does, or a Jira key embedded in the name (`Test_THISE_220_...`).
