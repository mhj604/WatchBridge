# 0.5.33 / build 67 — initial foreground evidence and notification-content handling

## Investigation scope

The November 25 build-66 REA records distinguish initial foreground entry from repeated inactive/active transitions. Foreground callbacks at 12:42:19 and 12:50:39 KST followed notification-detail receipt by approximately 17 and 4 seconds. Receipt is neither confirmed view appearance nor a tap. It does not establish notification causation or a physical user action. BLE was already authenticated and location activity eligible. [Earlier observations](MAIN_SCREEN_2026-11-25_EN.md).

Further REA retrieval and installation failed at the Mac–Watch developer tunnel (`CoreDevice 4000 / RemotePairing 1001`). Restarting only the owner's Mac user-level device services did not restore access. Mac Bluetooth was on; Wi-Fi IPv6 was automatic with a link-local address. IPv6 being disabled is not the explanation. A paired/available listing is not successful app-container access.

## Behavior change

`CompactNotificationController` previously used the default `isInteractive=false`, allowing notification-content taps to perform the default app-opening action. It now uses true and a content-only tap handler: **tapping the custom source-icon notification's content no longer opens the connection main screen**. It only records a fixed marker. Explicit app-icon/sash launches and native system notification interfaces retain their watchOS behavior. This is a concrete entry-path mitigation, not proof that a tap caused the reported incident.

Notification categories now enable `customDismissAction`. Without it the existing dismiss callback could not receive explicit dismissal actions. Handling dismissal only records an event; it invokes no vehicle command or screen presentation.

## Automatic evidence

- The initial main-interface foreground callback freezes 64 preceding display events and 32 connection events in `watchbridge-foreground-episodes.json`. Repeated wrist activations retain the same episode and cannot replace its initial context. Retain 32 episodes.
- Associate the first main-scene activation, nearby notification/location events, later explicit entry markers and background return with that episode. Association does not establish causation.
- Distinguish notification-detail view appearance/disappearance and foreground notification presentation from receipt alone.
- Record each location activity creation/restoration request with an object ID before creating it. Preserve the existing object lifetime, authorization, rejoin and connection behavior.
- Add SwiftUI URL/web-user-activity entry markers. This is not complete OS-trigger visibility. No URLs, notification content, activity payloads or coordinates are recorded.

## Deployment and remaining work

Source and signed build are **0.5.33 / 67**. The owner's last successful installation remains **0.5.32 / 66**; the new installation awaits developer connectivity. Private weekly-renewal source/state still target installed build 66. Registration, vehicle assignments, BLE/crypto and background connection mechanisms remain unchanged.

After the owner reconnected Watch Wi-Fi and prepared developer connectivity, both status and display retrieval still failed at the same tunnel (`ev_7c2daed097734c06206c1bf51f345699869c209a900184f1c0420392cfb5d19f`, `ev_78d1cfcb07e3a41baaf079912f66b84d39f56de22717c222b651c04dcc025583`). The Galaxy ADB device list was also empty, leaving no connected alternative app-record path. No app-launch command or BLE-service stop was issued during this follow-up. Mac Device Hub was closed.

**The initial OS foreground trigger remains unknown.** This change closes a known content-tap entry route and improves first-transition evidence. It does not establish complete resolution or a new successful physical-device background observation. No system logs, administrator authentication, vehicle commands or separate QA were used.

REA evidence: retrieval `ev_d77b82013b7c8a03dcd9a2e921a2628ff8a70b1e23e63aee86103f6ce0e5ae84`, installation failure `ev_0b3317ec86f2e4543a844e7c1bd01e3e8940e2b08d98486733c784a1b222329b`, retrieval after service restart `ev_805056439f1ffa4340c0f9cca0fb019e59999c2f68e1a3a6b1878e8083d8569a`. Raw evidence remains local.

Primary sources: [notification activation behavior](https://developer.apple.com/documentation/watchos-apps/presenting-notifications-on-apple-watch), [default isInteractive value](https://developer.apple.com/documentation/swiftui/wkusernotificationhostingcontroller/isinteractive), [explicit-dismissal requirements](https://developer.apple.com/documentation/usernotifications/unnotificationdismissactionidentifier), [SwiftUI user activity](https://developer.apple.com/documentation/watchkit/handling-user-activity).
