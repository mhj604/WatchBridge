# November 24 — preceding-day vehicle-panel investigation

The owner confirmed that the preceding day's unexpected screen was the vehicle-control panel. REA retrieved current app status, activation and display files for comparison with locally preserved captures. This investigation did not launch the app, open a panel or reinstall anything.

The preceding day's records are build 64. Retained records contain no new `vehicle.panel.widget`, `vehicle.panel.in-app` or `vehicle.quick.intent` entry marker. They do contain reactivations of the same process retaining a widget-entry marker from the 21st. Rotation and missing historical records prevent an absolute no-new-request claim.

Build 64 source did not clear `presented=true` on background transitions. This path and the owner's screen description are consistent with **redisplay of a retained vehicle panel**. The old `renderedSurface` inferred surface from a past entry rather than observing actual sheet/view state. Reactivation counts are not physical-screen counts. The precise OS foregrounding trigger remains unresolved.

Cleanup of this path is included in **0.5.32 / build 66**, installed today. Current build 66 status reports authenticated background connectivity and false presentation/view flags. The retrieved build 66 display interval has no vehicle-entry request; dedicated vehicle files were not yet present. This establishes neither absence of future recurrence nor visibility into every OS transition. [Deployment and evidence scope](DEPLOYMENT_0.5.32_EN.md).

REA evidence: status `ev_ef07a994f78d94813025e976d17101db8647ec8f695372cf6cc88843fae50447`, activations `ev_038e0196ba7cae12cbb8838deab968405b7f9551f9186ef86be6bb3a9ae5a172`, display `ev_e70f0793098d1952b5e339887d189f08276f1b0298f75109b6e6b0e119d15e15`. Raw records and setting values remain local.
