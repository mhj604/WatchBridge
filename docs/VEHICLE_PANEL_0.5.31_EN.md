# Watch 0.5.31 — dismiss retained vehicle panels in the background

Watch/widget source **0.5.31 / build 65**; Android **0.6.23 / code 45**. The build completed; subsequent deployment results are recorded below.

## Narrowed issue

The owner confirmed that the unexpected screen on November 23 was the **vehicle-control panel**. Automatic records retained a November 21 18:13 widget-entry marker without a later panel-dismiss marker. The same authenticated, connected process reactivated on November 23. [App-owned evidence](DISPLAY_OBSERVATION_2026-11-23_EN.md).

The sheet is driven by `VehicleQuickRouter.presented`. Existing code set it for explicit widget/in-app requests but did not clear it on background transitions, allowing the old panel to survive foreground restoration. This explains a persistent vehicle-panel path; it does not establish the private OS trigger that brought the app forward.

## Changes

- Dismiss a previously active panel when SwiftUI enters background; leave ordinary inactive transitions alone.
- Preserve a new widget request until its first active scene rather than dismissing it during startup background transitions.
- Distinguish automatic background dismissal from user dismissal. Automatic sheet/view callbacks do not additionally cancel an already user-initiated command preparation or response. Existing user dismissal/navigation cancellation remains. Dismissal creates no commands and retries none.
- Observe actual `presented` changes as panel-presented/panel-hidden events plus background-dismissal markers. App diagnostics include `vehiclePanelPresented`; this is presentation intent, not a direct visual observation.

BLE, location sessions, cryptographic and installation identifiers, registration and vehicle-button assignments remain intact. No system logs, administrator authentication, real vehicle commands or separate range/lock tests are used. Deployment records use app-owned files and REA captures.

## Deployment status

Build completed. The Mac–watch development tunnel timed out again; connection/unlock preparation is pending. Until installation succeeds, the owner's installed build 64 and private weekly-renewal source remain aligned. Only successful installation will update that metadata to build 65.
