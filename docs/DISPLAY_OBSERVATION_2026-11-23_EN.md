# Display reappearance observation — 2026-11-23

Watch 0.5.30 / build 64; Android 0.6.23 / code 45. No app behavior or installed build changed.

## App-owned evidence

At approximately 15:10 KST, the owner reported an unexpected screen appearance roughly one hour earlier, without pressing Report screen issue. The development tunnel initially timed out. It subsequently recovered after reconnecting the existing Mac developer pairing and discovering endpoints; no single step is claimed to have caused recovery. The owner's same-network statement remains accepted.

The display file contained 945 entries, including 689 build-64 entries from the same process started on November 21 at 18:10 KST. A separate activation summary was retrieved. Automatic logging therefore worked without an incident-button press.

| KST | Observation |
| --- | --- |
| 13:58:18 | Main app entered background |
| 14:01:11.394 | Custom notification controller didReceive |
| 14:01:22.313 | Main app will-enter-foreground |
| 14:01:28.971 | SwiftUI scene.active |
| 14:09:42.458 | Notification detail didReceive |
| 14:09:50.603 | scene.active |
| 14:13:01 | Main app returned to background |
| 14:15:56.444 | Notification detail didReceive |
| 14:16:00.859 | Main app will-enter-foreground |
| 14:18:15.213 | scene.active |

All listed transition samples were connected and authenticated. There was no new process launch, notification-open response or new widget-entry marker in this interval. The last widget marker was November 21 at 18:13, not a recent tap.

## Interpretation and limits

The observed mechanism is foreground return and reactivation of the existing app. Notification-detail delivery preceded several main-app transitions, but temporal sequence does not establish a trigger. The approximate incident time cannot identify one specific transition as the reported event.

Notification didReceive does not mean the user tapped it. The retained vehicle-panel renderedSurface value reflects an old entry marker, not proof of the actual screen. Native active and SwiftUI inactive also coexist in some samples.

[Apple life-cycle documentation](https://developer.apple.com/documentation/watchkit/handling-common-state-transitions) distinguishes main-interface and supplementary notification callbacks and warns that app and interface state can differ. [Always On documentation](https://developer.apple.com/documentation/watchos-apps/designing-your-app-for-the-always-on-state) describes retained onscreen behavior. Neither establishes that a specific location session or private OS restoration policy caused this incident.

Status: automatic logs retrieved and existing-process foreground return confirmed; immediate trigger unresolved. No speculative location/BLE rollback was applied. The owner was asked which screen appeared. No system logs, administrator authentication, vehicle commands or watch-app launch commands were used.

REA evidence: display `ev_e8bff0ffd6113167721197b331663a1184a82de0e1a75aa0fdbb6c60226aa86d`; summaries `ev_7ec58f5569f379420b2d223b120f3466e45195dea69795c7a651549e76a1999a`; app state `ev_b081ad80a2c379a290c3805e21103704610dafbfd256e02672473928e050309b`. REA captured Apple devicectl file reads. Device addresses, keys and raw records remain private.
