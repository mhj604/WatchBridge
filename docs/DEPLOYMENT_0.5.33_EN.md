# 0.5.33 / build 67 — installed on November 25

The Mac–Watch developer channel became usable again. Existing records were preserved before installing **Watch app/widget 0.5.33 / build 67** in place. Android remains **0.6.23 / code 45**. No further network change or developer re-pairing was performed immediately before recovery, so no specific recovery action is established as the cause.

## Installed behavior and runtime

- Applied [notification-content handling and initial foreground evidence](FOREGROUND_ENTRY_0.5.33_EN.md). Custom source-icon notification-content taps stay in the notification; explicit icon/sash launches retain OS behavior.
- Preserved prior app state, 948 display events and preferences locally. Raw records and setting values remain private.
- Retained peer registration, profile, vehicle mappings and connection-maintenance preferences. Bundle/team/keychain/BLE/crypto identifiers are unchanged.
- The new process recorded Bluetooth restoration. **No app-launch command or manual app opening was performed during this deployment.**
- At 16:35 KST, build 67 reported connected/authenticated true, SwiftUI background and native application inactive. Do not relabel this as native background or proof of no physical presentation. Location activity was `restore-requested`, not a new long-term continuity result.
- Schema-4 events include location-object restoration, Bluetooth restoration, main-view construction and scene background. No main scene.active appears in the initial retrieved interval. With no foreground episode yet, its dedicated file had not been created. This describes the observed interval, not a guarantee against recurrence.
- A naturally arriving detail notification recorded appearance/disappearance at 16:36:21–16:36:32 KST. The interval retrieved at 16:38 still contained no main scene.active, with connected/authenticated true. This demonstrates the new distinction between notification presentation and main activation; no content-tap experiment was performed.

## Additional pre-update observation

Build-66 records contain **`notification.open` at 14:58:28 KST**, followed approximately 0.9 seconds later by main scene.active. This is one observed default notification-opening action. **Its connection to the 13:16 incident, and whether it originated in content or the icon/sash, are unknown.** It does not establish the initial unexpected-opening cause or a physical tap by the owner.

## Weekly signing

Aligned the private renewal source and installed metadata to committed build-67 source `4af189d`, with a local backup. Preserve the **seven-day Friday 16:00 schedule**. Profiles still expire **2026-11-27 19:52 KST**, so no new signing-completion notice was generated.

## REA evidence and limits

- Previous state: `ev_7a7601c640185ece5f01ebf14601ae545f9191828665af0e3f5e2dcd2c6341f2`
- Previous display journal: `ev_9a2c4cb0a122f3ab0bd59e4ac5dc58196c0da870d29b56521cac15df44e7a3c4`
- Successful installation: `ev_87c9d4a25791ac913f0b4c33107936a6c638ba5a6a4905634dd3cda2afc17744`
- New app state: `ev_9e7e2f4a50c0e60337d5aa3fa04f957cfb91246a956db5d0b3168e778bdac9f6`
- New display journal: `ev_09682a7464334f85d8604046b21a91593064c0ff9d6b8f12c18f31b345e54153`
- 16:38 state/display: `ev_30d747395d9692c5417ad2e82b9390ba1faa9b46602b28ab68903b5a6dd42266`, `ev_242fd690b16d94d94a4bc8d62f0cb21a0dd19b01a319f1574d3205023a27a52e`

The initial OS foreground trigger remains unknown. This completes deployment of a known entry-path mitigation and evidence improvements, not complete resolution of unexpected presentation. No BLE-service stop, unpairing, system logs, administrator password, vehicle commands or separate QA were used.
