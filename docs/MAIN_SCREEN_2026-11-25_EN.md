# November 25 — main screen reappearance

The owner reported an unexpected connection-status main screen rather than the vehicle panel. REA retrieved status, display events, activation summaries and connection events from installed **0.5.32 / build 66**. No app launch, installation or presentation command was issued during this investigation.

## Observations

- The report was captured at 13:16 KST; the nearest recorded main-scene activation was **13:13:48 KST**. The owner did not specify the occurrence time, so correspondence is not certain.
- The same process has been running since yesterday's installation. This was not a new process launch or a vehicle-panel request. Vehicle presentation and view-visible flags were false.
- A foreground transition occurred at 12:50:39, followed by repeated inactive/active transitions. At 13:13:48, inactive → active → scene.active was recorded; background followed at 13:13:52.
- The 320 retained display events for this build contain no notification-open, user-activity or vehicle-widget entry marker. The 27 scene.active records are not a count of confirmed unexpected openings.
- BLE was already connected and authenticated during the relevant activations, and location activity was eligible. A reconnect or newly created location session causing the presentation is not established.

## Interpretation and remaining work

The repeated transitions fit watchOS frontmost-app behavior. Apple describes an inactive frontmost app becoming active on wrist raise, and returning to background when dismissed with the Crown. Location activity apps can behave similarly. [Apple documentation](https://developer.apple.com/documentation/watchkit/taking-advantage-of-frontmost-app-state).

This does not establish the trigger for the initial foreground transition. Do not attribute it conclusively to location activity, treat the retained-vehicle-panel fix as a main-screen fix, or infer a physical notification/widget tap. **Unexpected main-screen presentation remains unresolved and is again an active investigation.** This update changes documentation only; installed versions and app behavior remain unchanged.

REA evidence: status `ev_e14ee7628652052255b343802802523d9241c1bdc528591e5eebd3b725948f63`, display `ev_7d0c0e166832fe71f4f0564c243c7e0de510d660310c7c9e17b821733d8c73ad`, connection `ev_952c1864c4ee337f39f3990584b834578302e3574cb2b9e06e7a4b428e09c633`. Raw records and device details remain local.
