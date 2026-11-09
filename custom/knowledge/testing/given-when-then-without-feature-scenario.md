---
bc-version: [all]
domain: testing
keywords: [given, when, then, feature, scenario, tags, comments, bdd, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: mark tests with GIVEN/WHEN/THEN; FEATURE and SCENARIO are optional

## Description

KOLLAB policy, not a platform rule. KOLLAB test codeunits structure every test body with `// [GIVEN]`, `// [WHEN]` and `// [THEN]` comments, but do not require the `[FEATURE]` and `[SCENARIO]` tags. The business intent of a test is carried by the codeunit name (`"<Feature> Test"`) and the procedure name (`Test_NN_<Subject>_<Outcome>`, see `test-procedure-naming-numbered-outcome.md`), which together play the role `[FEATURE]` and `[SCENARIO]` play in the Microsoft corpus. This file overrides `microsoft/knowledge/testing/test-feature-scenario-tags.md` for KOLLAB apps.

## Best Practice

Every `[Test]` procedure marks its setup with `// [GIVEN]`, the single action under test with `// [WHEN]`, and the assertions with `// [THEN]`, always with square brackets. Several consecutive `[GIVEN]` lines are fine when the setup has several steps. Each marker is followed by a short description in plain language. `[SCENARIO]` and `[FEATURE]` may be added when they help — for example a `[SCENARIO]` carrying the Jira key the test covers — but their absence is not a finding.

## Anti Pattern

Reporting a missing `[FEATURE]` or `[SCENARIO]` tag on a KOLLAB test codeunit — that is a false positive under this policy. What is a defect: a test body without `[GIVEN]`/`[WHEN]`/`[THEN]` markers, markers written without brackets (`// GIVEN`), or a placeholder marker with no description (`// [THEN] Then`).
