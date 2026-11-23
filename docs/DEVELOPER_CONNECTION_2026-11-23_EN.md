# 2026-11-23 — Mac developer-connection failure scope

This concerns the owner's Mac developer connection, not a confirmed cause of Galaxy–Watch BLE behavior or unexpected vehicle-panel activation.

## Observations

- Developer Mode, stored Mac developer pairing and Mac Bluetooth are enabled.
- CoreDevice changed from disconnected to unavailable. The last successful connection was November 23 at 15:27 KST.
- REA app-file retrieval and installation failed with CoreDevice 4000 / RemotePairingError 1001.
- Subsequent retrieval failed immediately with **4016**: `coreDeviceServicesLoaded`, `remoteServiceDiscoveryTrustedConnectivityAvailable` and `powerAssertionTaken` could not be acquired; `CurrentlyAssertableStates` was empty. This alone establishes neither low battery nor passcode lock as the cause.
- Device-details commands may return cached data with exit code 0. Their success outcome does not prove a live connection.
- No remote-pairing advertisement appeared in brief Bonjour observation windows. An rp-tunnel endpoint was found but not identified as the watch; its advertised TCP port refused a connection.
- A local route and IPv6 link-local address exist. Device Hub and remotepairingd are allowed by the firewall. VPN tunnels are disconnected while network extensions remain registered as active; registration alone does not prove interference.

## Conclusion and remaining uncertainty

The immediate failure is in **Apple developer-service discovery, trusted connectivity and tunnel establishment**, before app data access or installation. It is not evidence of a WatchBridge app or APK defect. Watch-side developer-service state, Mac network-filter interference and negotiated endpoint freshness remain unseparated.

[A developer report with watchOS 27.2 and Ultra 2](https://developer.apple.com/forums/thread/848740) describes reconnection trouble, but neither confirms the same defect here nor constitutes Apple's official diagnosis.

REA evidence: `ev_1aeed59090846d1e0341c9358900849c1924aed472a8c101b640d640f4ea05ff`, `ev_7ca442a529c1a86334bd85b37166275dd578204656edf8fefca68d2f0d34eee9`, `ev_c458242dfabed511a7025da58a03c694c7119a695a32f961649d7d21229d065e`. Raw evidence stays local.

No registration reset, protection-setting change, system-log collection, administrator authentication or vehicle command was performed. Mac device discovery was closed. Installed Watch remains 0.5.30 / 64; 0.5.32 / 66 is pending installation.
