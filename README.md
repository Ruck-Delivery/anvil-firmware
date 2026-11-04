# anvil-firmware

Public Anvil firmware OTA binaries (no app source). The Ruck app installs the latest release; each release's `anvil-manifest.json` names the oldest app that can drive it (`minAppVersion`).

## Which Ruck app works with which firmware

| App ↓ · Firmware → | 2026.11.04.1 | 2026.11.04 | 2026.11.02 | 2026.11.01 | 2026.10.31 | 2026.10.30 | 2026.10.20 | 2026.10.11 |
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| **1.45.0** | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ |
| **1.44.0** | ⚠️ | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ |
| **1.43.0** | ⚠️ | ⚠️ | ✅ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ |
| **1.42.0** | ⚠️ | ⚠️ | ⚠️ | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ |
| **1.41.0** | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ⚠️ | ✅ | ⚠️ | ⚠️ |
| **1.40.0** | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ✅ | ✅ |
| **1.39.0** | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ⚠️ | ✅ |
| **1.38.0** | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ⛔ | ⚠️ | ✅ |

✅ everything works · ⚠️ works, and a feature waits for the older side to update (the release tables say which) · ⛔ not together: the Anvil holds the update at "Update the Ruck app first" · ❔ published without a check

## Firmware releases

| Firmware | Published | Needs app | Everything from app | An older app misses | Breaking | Checked against apps |
|---|---|---|---|---|---|---|
| **2026.11.04.1** | 2026-11-04 | 1.41.0 | 1.45.0 | Apps before 1.45.0: after two missed nights Anvil now catches up at any hour, but these apps still show a clock time ("Installs tonight at ...") and offer Not tonight, which then only restarts the count. The update installs either way, and holding D0 during a silent update switches Anvil on in every app. 1.43.0 and 1.42.0 also miss what 2026.11.04 added. | no | 1.44.0, 1.43.0, 1.42.0 (code review) |
| **2026.11.04** | 2026-11-04 | 1.41.0 | 1.44.0 | Apps 1.41.0 to 1.43.0: no Vibration switch, so an Anvil the newer app set to stay still stays still (a factory reset turns it back on), and its reset and error reports don't reach the cloud through the app. 1.41.0 and 1.42.0 also miss what 2026.11.02 added; 1.41.0 has no self-test. | no | 1.43.0, 1.42.0, 1.41.0 (code review) |
| **2026.11.02** | 2026-11-02 | 1.41.0 | 1.43.0 | 1.41.0 and 1.42.0: no caller announcement (the call only rings), no factory reset from the app, and after a reset with the buttons they keep trying to reconnect the wiped Anvil. 1.41.0: no self-test. | no | 1.43.0, 1.42.0, 1.41.0 (code review) |
| **2026.11.01** | 2026-11-01 | 1.41.0 | 1.42.0 | 1.41.0: no self-test in the device sheet. | no | 1.42.0, 1.41.0, 1.40.0 (code review) |
| **2026.10.31** | 2026-10-31 | 1.41.0 | 1.42.0 | 1.41.0: no self-test in the device sheet. | no | 1.42.0, 1.41.0, 1.40.0 (code review) |
| **2026.10.30** | 2026-10-30 | 1.41.0 | 1.41.0 | nothing | The speaker chip now rests Bluetooth Classic after a minute unused. Apps before 1.41.0 can't wake it, so a reply after a rest is silent (or in the phone's earpiece) and 2 to 4 s late. Gated: the manifest needs app 1.41.0. | 1.41.0, 1.40.0, 1.39.0 (code review) |
| **2026.10.20** | 2026-10-20 | 1.0.0 | 1.40.0 | Before 1.40.0: an open device or update sheet keeps the Anvil on Wi-Fi (about 60 mA more), because it asks for the full status every 15 s. | no | 1.40.0, 1.39.0, 1.38.0 (code review) |
| **2026.10.11** | 2026-10-11 | 1.0.0 | 1.38.0 | Before 1.38.0: the Anvil's battery history and SD minute log don't reach the cloud. | no | 1.38.0, 1.37.1, 1.37.0 (code review) |

## Ruck app releases

| App | Published | Needs firmware | Everything from firmware | Older firmware misses | Breaking | Checked against firmware |
|---|---|---|---|---|---|---|
| **1.45.0** | 2026-11-04 | any | 2026.11.04.1 | Before 2026.11.04.1: Anvil never catches up after missed nights, so the "Installs next time Anvil is charging near Wi-Fi it knows" line never shows. Before 2026.11.04: the Vibration switch does nothing, and the Anvil's reset and error reports don't reach the cloud. Before 2026.11.02: no caller announcement or factory reset from the app. Before 2026.10.31: no self-test. Before 2026.10.30: no head start, stored voice notes, video review or overnight update. | no | 2026.11.04, 2026.11.02, 2026.11.01 (code review) |
| **1.44.0** | 2026-11-04 | any | 2026.11.04 | Before 2026.11.04: the Vibration switch does nothing, and the Anvil's reset and error reports don't reach the cloud. Before 2026.11.02: no caller announcement or factory reset from the app. Before 2026.10.31: no self-test. Before 2026.10.30: no head start, stored voice notes, video review or overnight update. | no | 2026.11.02, 2026.11.01, 2026.10.31 (code review) |
| **1.43.0** | 2026-11-02 | any | 2026.11.02 | Before 2026.11.02: no caller announcement or factory reset from the app. Before 2026.10.31: no self-test. Before 2026.10.30: no head start, stored voice notes, video review or overnight update. | no | 2026.11.02, 2026.11.01, 2026.10.31 (code review) |
| **1.42.0** | 2026-10-31 | any | 2026.10.31 | Before 2026.10.31: no self-test. Before 2026.10.30: no head start, stored voice notes, video review or overnight update. | no | 2026.10.31, 2026.10.30, 2026.10.20 (code review) |
| **1.41.0** | 2026-10-30 | any | 2026.10.30 | Before 2026.10.30: no head start (a press waits for the voice link), stored voice notes, video review or overnight update. | no | 2026.10.30, 2026.10.20, 2026.10.11 (code review) |
| **1.40.0** | 2026-10-21 | any | any | nothing | no | 2026.10.20, 2026.10.11, 2026.10.10 (code review) |
| **1.39.0** | 2026-10-12 | any | 2026.10.11 | Before 2026.10.11: the Anvil's battery history and SD minute log don't reach the cloud. | no | 2026.10.11, 2026.10.10, 2026.10.09.2 (code review) |
| **1.38.0** | 2026-10-11 | any | 2026.10.11 | Before 2026.10.11: the Anvil's battery history and SD minute log don't reach the cloud. | no | 2026.10.11, 2026.10.10, 2026.10.09.2 (code review) |

## Breaking changes

- **Firmware 2026.10.30** (2026-10-30): The speaker chip now rests Bluetooth Classic after a minute unused. Apps before 1.41.0 can't wake it, so a reply after a rest is silent (or in the phone's earpiece) and 2 to 4 s late. Gated: the manifest needs app 1.41.0.

Refreshed on every Ruck app and Anvil firmware release.
