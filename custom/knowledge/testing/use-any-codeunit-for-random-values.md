---
bc-version: [all]
domain: testing
keywords: [any, library-random, random, test-data, randint, alphanumerictext, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: use the Any codeunit for random test values

## Description

KOLLAB policy, not a platform rule. Both the `Any` codeunit (Microsoft app "Any") and `Library - Random` produce random values, and KOLLAB repositories have mixed them, sometimes in the same file. KOLLAB uses `Any` as the single standard so tests read the same across customers: `Any.IntegerInRange`, `Any.DecimalInRange`, `Any.AlphanumericText` and related procedures. `Library - Random` is not wrong, but it is not the house choice.

## Best Practice

Declare `Any: Codeunit Any` and use it for incidental random values. Test apps that need random values take a dependency on the "Any" app. Values that define the expected outcome — amounts at a rounding boundary, quantities that trigger a threshold, specific dates — stay explicit, as `microsoft/knowledge/testing/test-data-must-be-random-and-complete.md` describes. In existing codeunits that already use `Library - Random`, do not mix: either keep it or convert the whole codeunit.

## Anti Pattern

New test code that uses `LibraryRandom.RandInt`, `RandDec` or `RandText`, or a single codeunit that uses both `Any` and `Library - Random`.
