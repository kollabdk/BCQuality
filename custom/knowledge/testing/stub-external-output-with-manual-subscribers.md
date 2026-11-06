---
bc-version: [all]
domain: testing
keywords: [bindsubscription, eventsubscriberinstance, manual, ishandled, email, http, stub, kollab]
technologies: [al]
countries: [w1]
application-area: [all]
---

# KOLLAB: stub external output with a manual subscriber codeunit

## Description

KOLLAB policy. Code under test often sends email, writes files or blobs, or calls an external service. In a test that output must not leave the environment, and the test usually needs to inspect what would have been sent. KOLLAB tests stub it by subscribing to the app's own `IsHandled` or `OnBefore...` event from a codeunit with `EventSubscriberInstance = Manual`, binding it only for the tests that need it. A manual subscriber is active only while it is bound with `BindSubscription` and the bound variable is in scope, so it cannot affect other tests or production.

## Best Practice

Put the subscribers in a dedicated test-app codeunit with `EventSubscriberInstance = Manual` (or in the test codeunit itself with the same property, bound with `BindSubscription(this)`). Set `IsHandled := true` and store what would have been sent in global variables the test can assert on. Call `BindSubscription` in the `[GIVEN]` block and `UnbindSubscription` at the end of the test, because a binding on a global variable otherwise survives into the next test in the same codeunit. When the app has no event to hook, add an `IsHandled` integration event in the app rather than letting the test call the external service.

## Anti Pattern

A test that sends real email or calls a real external endpoint, a subscriber codeunit with the default `EventSubscriberInstance = StaticAutomatic` in a test app (it intercepts every test and every user), or a `BindSubscription` on a global variable with no matching `UnbindSubscription`.
