# Watch 0.5.32 / build 66 — deployment on 2026-11-24

The Mac–watch developer channel became usable and **Watch app/widget 0.5.32 / build 66 were installed in place**. Android remains 0.6.23 / code 45. This transfer and deployment succeeded wirelessly without an iPhone USB connection or another network. Connectivity returned after the earlier developer-pairing rebuild, but neither its underlying failure cause nor a particular recovery action is established.

## Included behavior

This installs both [retained-panel cleanup from 0.5.31](VEHICLE_PANEL_0.5.31_EN.md) and [automatic evidence from 0.5.32](VEHICLE_EVIDENCE_0.5.32_EN.md). Panel requests receive IDs, source paths and timestamps; presentation intent is separate from view callbacks. Vehicle-view appearance or reactivation with a retained panel automatically freezes preceding records without a Report screen issue button press.

## Deployment and initial execution

- Preserved 1,024 existing display events, 207 activation records, app state and preferences locally before installation. Raw journals and setting values are not published.
- Updated build 64 to 66 using unchanged bundle/team/storage identifiers. Saved peer registration, vehicle assignments and connection-maintenance preferences matched before and after deployment.
- Requested launch with `--no-activate`. The new process had already started through Bluetooth restoration, so its environment records `launchSource=unspecified`. The launch flag alone does not prove the physical screen was never visible.
- At 15:33 KST, app-owned status reported build 66, connected/authenticated true, background scene/application and false panel presentation/view flags. Location activity was `restore-requested`; this is not a long-term continuity result.
- No intentional panel opening, vehicle command, range experiment or extended-lock run was performed. The initial unexpected-opening cause remains unresolved.

Build 64 activation history includes reactivations classified as the vehicle surface long after an old widget-entry marker. Those are not evidence of a fresh physical tap. Rotation removed some earlier general events. The new dedicated panel journal and automatic snapshots improve attribution and retention.

## Weekly signing

Aligned the private renewal source and installed metadata with committed build 66. The **seven-day Friday 16:00 schedule remains unchanged**. Existing provisioning still expires **2026-11-27 19:52 KST**. This was a feature deployment, not an expiration extension; it generated no new signing-completion notice.

## REA evidence

- Original display file: `ev_64599d6ac6c522f7d0a2fca0b300ff0c5c74fec8b0e53ae6562d83ea18e5a9cb`
- Installation: `ev_4e47cf25b1c52cc968f56a3c5b84101da74cc96d291181279c3cb210967ae81d`
- No-activate launch: `ev_1ba2faaef603382b667677a6a4a44f2d886ec1ef8f5892964b8cdf2796761ee8`
- New app status: `ev_7117741802b1e848d3460408ace2ed8edeb805e33a0895ba478e73a39e0e0027`
- New display journal: `ev_7dbd7cf048d2ee0443f868ed6ef5cba9e79ab206be8ccaf048d23d03c04e4510`

These contain inner command exit code 0 and actual transfer/installation results. No system logs or administrator credentials were used.
