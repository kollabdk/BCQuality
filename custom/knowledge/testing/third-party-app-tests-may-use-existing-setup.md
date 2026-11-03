---
bc-version: [all]
domain: testing
keywords: [third-party, aptean, fdw, existing-data, sandbox, setup, master-data, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: tests of third-party app functionality may use existing setup

## Description

KOLLAB policy and a negative clarification. Third-party apps such as Aptean Food & Beverage ship no test libraries, and their setup (catch-weight items, lot attributes, landing and production setup) is too large to build from scratch in each test. KOLLAB tests of functionality built on such apps — typically the `FDW`-prefixed test codeunits in a separate test app — therefore run against a configured customer sandbox and may use existing setup and master data. This file overrides `microsoft/knowledge/testing/test-data-must-be-random-and-complete.md` and `microsoft/knowledge/testing/use-library-codeunits-for-test-fixtures.md` for those test codeunits only.

## Best Practice

Do not flag existing-data lookups in a test codeunit that tests third-party functionality. The test must still make its dependency explicit: check the required setup with `TestField` or an assertion at the start of the `[GIVEN]` block, so a missing configuration fails with a clear message instead of a confusing error later. Read the data it depends on through a small, named `Get*` helper rather than literals scattered through the test body. Records that the base app can create — customers, vendors, locations without third-party fields — should still be created with the standard Library codeunits.

## Anti Pattern

The false positive: reporting "test assumes existing records" on an `FDW` test codeunit that checks its setup first. The real defect: a third-party test that uses existing data with no precondition check, hardcoded customer or item numbers repeated throughout the test body, or a test of base-app-only functionality that relies on sandbox data.
