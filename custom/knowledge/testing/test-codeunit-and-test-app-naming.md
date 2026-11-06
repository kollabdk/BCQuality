---
bc-version: [all]
domain: testing
keywords: [naming, test-codeunit, test-app, id-range, file-name, fdw, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: test codeunit names, file names and test app ID ranges

## Description

KOLLAB policy, not a platform rule. Tests live in a separate test app next to each app they cover (for example `<App>\test` beside `<App>\app`). Test codeunits are named `"<Feature> Test"` with spaces between words, and the file is `<Name>Test.Codeunit.al` following the CRS file-naming pattern. Tests that cover functionality built on Aptean Food & Beverage objects carry the `FDW` prefix (`"FDW Landing Test"`) so they can be told apart from tests of the same feature without Aptean. Each test app has its own ID range starting at 99000, and test apps in the same repository must not overlap, because they can be published to the same environment.

## Best Practice

One feature per test codeunit. Name the codeunit after the feature, not the object it happens to call. Keep the `.Codeunit.al` casing consistent. When adding a test app to a repository, choose an ID range that no other test app in that repository already declares (for example 99000–99099 for the base test app, 99100–99199 for the next one), and keep every codeunit inside its app's declared range.

## Anti Pattern

Two test apps in one repository that declare the same ID range or contain codeunits with the same ID. Codeunit names without spaces (`"CustReqDocumentTypeTest"`), missing spaces after the prefix (`"FDWFixed Lot Catch Weight Test"`), file names in another pattern (`Cod99100.<Name>.al`), or inconsistent casing (`.codeunit.al`).
