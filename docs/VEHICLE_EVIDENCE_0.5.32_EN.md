# Watch 0.5.32 — automatic vehicle-panel evidence

**Follow-up — 2026-11-24:** Build 66 installation and background launch completed. November 23 failure/pending statements below describe that earlier snapshot. [Latest deployment](DEPLOYMENT_0.5.32_EN.md).

Watch/widget source **0.5.32 / build 66**; Android remains 0.6.23 / code 45.

## What remains unknown

The owner clarified that they did not tap the vehicle-control panel. The old `vehicle.panel.widget` marker proves entry into `OpenVehicleControls.perform`, not a physical tap. Build 65 addresses retained presentation state; it does not establish why the panel first opened without a tap or why watchOS foregrounded the app.

## Automatic records

- Every panel-opening request receives a new request ID and timestamp, including repeat requests while already presented. Records include the preceding presentation state, process/build, lifecycle and connection state.
- Sources distinguish `OpenVehicleControls.perform`, `RunVehicleQuickControl.perform`, the main-app button, quick-panel buttons and all-controls buttons. Only internal control enum values are stored; no vehicle details or notification bodies are added.
- Sheet presentation intent is separate from SwiftUI view appearance/disappearance. Settings and all-controls navigation also leave markers. These callbacks are not direct observations of physical display contents or touches.
- Vehicle-view appearance or app reactivation with a retained panel automatically freezes the preceding 48 display events and 16 vehicle events. No Report screen issue button press is required.

App Documents retain 256 records in `watchbridge-vehicle-panels.json` and 16 snapshots in `watchbridge-vehicle-panel-snapshots.json`, replacing the oldest entries at those limits. Existing display and activation journals remain. REA can retrieve these app-owned files after recurrence to distinguish a new request from restored presentation state. Failed writes, times when the process was not executing, and records beyond retention remain unobservable.

## Deployment

Build completed. Build 65 installation attempts failed with a Mac–watch developer-tunnel timeout. The owner's installed app and private weekly-renewal source stay at 0.5.30 / 64 until an actual installation succeeds. Build 66 deployment results follow below. Registration, vehicle assignments, BLE, location activity and the signing schedule remain intact.

### November 23 installation outcome

REA installation evidence `ev_6f7ffba46f6809ad373d792397de503d40d9004d67e48c6753c6039105a25379` contains inner command exit code 1: `CoreDeviceError 4000 / RemotePairingError 1001`, a developer-network tunnel timeout. **Build 66 is not deployed, and its automatic evidence feature is not yet running on the owner's watch.** Private renewal source and installed metadata remain at build 64. The Mac device-inspection window was closed.
