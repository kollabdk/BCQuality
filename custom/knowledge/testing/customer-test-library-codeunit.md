---
bc-version: [all]
domain: testing
keywords: [library-codeunit, fixtures, helper, test-library, reuse, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: shared fixtures go in a "Library - <Customer>" codeunit

## Description

KOLLAB policy, not a platform rule. It extends `microsoft/knowledge/testing/use-library-codeunits-for-test-fixtures.md`. The standard Microsoft Library codeunits create base-app records, but every KOLLAB customer app adds its own fields, setup tables and processes that tests need again and again — an item with lot tracking and the customer's item attributes, inventory with a given lot, setup values the customer app depends on. Each test app therefore has one codeunit named `"Library - <Customer>"` (for example `"Library - Thise"`, `"Library - Scandic Pelagic"`) that owns those fixtures, built on top of the standard Library codeunits.

## Best Practice

Reach for the standard Library codeunit first. When a fixture needs customer-specific fields or setup, or when two test codeunits build the same record the same way, move it into `"Library - <Customer>"` as a `Create*`, `Init*` or `Post*` procedure and call it from the tests. Shared setup that every test needs goes into an idempotent procedure on the library (for example `Initialize`) that can safely run before each test. Keep the library free of assertions and of the action under test — verification and the `[WHEN]` step belong in the test, which should still read top to bottom (see `test-reads-top-to-bottom-in-one-procedure.md`).

## Anti Pattern

The same `Init`/`Validate`/`Insert` sequence for a customer-specific record copied into several test codeunits, or a local helper in one test codeunit that duplicates a procedure the customer library already has. Also an anti-pattern: assertions inside library procedures, which hide what a test actually verifies.
