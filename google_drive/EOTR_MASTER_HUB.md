# 🦦 EOTR — MASTER HUB (Single Link Bootstrap)
### Eye's On The Road — pronounced "otter"
**This is the ONE link to paste at the start of any new chat with Arena.**

> When I paste this file's Google Drive link in a new chat, you (the assistant) must: 1) read THIS file fully, 2) list files in the shared hub folder, 3) read the latest project zips (Android + iOS), and 4) continue from where we left off — no re-asking about machines/tools/objective.

---

## 🤖 INSTRUCTIONS FOR FUTURE ASSISTANT
1. Fetch hub `eotr — Eye's On The Road (Shared Build Hub)` — list contents. Drive is source of truth.
2. Treat toolchain below as canonical — same tools for same APK/IPA.
3. Never ask again for 10s rule, otter icon, bundle ID.

## 📌 Project Identity
- **Name:** eotr (otter) / Eye's On The Road — bundle `com.eotr.eyesontheroad` for BOTH platforms — v1.0.0-otter
- **Inspiration:** prevent texting while driving — otter floating with phone = icon

## 🎯 Objective
Leverage accelerometer + GPS + gyroscope to set persistent rule: screen only usable after 10,000 ms level & still. Otherwise block/shield. (Original said "IF" → implemented as UNLESS — lock when moving).

## 🔒 10s Rule — Canonical SHARED (Android & iOS identical)
All 4 true 10s → UNLOCK else BLOCK:
| Signal | Threshold | Android | iOS |
| Accelerometer | |mag-9.81|<0.9 & var<0.35 | StationaryDetector.kt | StationaryDetector.swift |
| Gyroscope | <0.12 rad/s | StationaryDetector.kt | StationaryDetector.swift |
| GPS | <0.5 m/s & <30m | DrivingDetectionService.kt | DrivingDetectionManager.swift |
| Level | tilt <15° | computeTiltDegrees | tiltDegrees |
Loop 200ms, GPS 1s, variance 20. Emergency SOS/911 never blocked.

## 🛠️ Canonical Toolchains
**Android (APK):** Kotlin 1.9.22, Java17, Android Studio Hedgehog+, AGP8.2.2, Gradle8.6, compile34/min26/target34, play-services-location 21.2.0. Output app/build/outputs/apk/debug/app-debug.apk
**iOS (IPA):** Xcode15+, Swift5.9, SwiftUI, iOS16+, CMMotionManager 50Hz, CLLocationManager Always, FamilyControls+DeviceActivity+ManagedSettingsStore for shielding (App-Store-allowed), MDM for truly unbreakable. Output Archive → IPA.
**Shared:** otter PNG, hub https://drive.google.com/drive/folders/1q-gWovIsOkV1cqrfH-rip1DwpP9OhH4T

## 📂 Current State 2026-11-10 18:05 ET — NOW WITH iOS ✅
- Android zip 4.3MB https://drive.google.com/file/d/1e8Q4JjMjHD0NrZOhNSNF7l167vL7nixU/view?usp=drivesdk
- iOS zip 411KB https://drive.google.com/file/d/1CoJTDkVUqFxs6zcZXzbcW_xHzr3dijW9/view?usp=drivesdk — SwiftUI port, same logic, same thresholds, no drift. ScreenTimeManager no-ops if entitlement missing.
- Preview https://drive.google.com/file/d/1WykdX_ioRYkVJPspXb0OX9MBdE7Yg0ei/view?usp=drivesdk
- v2 hub https://drive.google.com/file/d/1DpxAnw2ZblxOz8-_mtTYUW56xL8QSr-k/view?usp=drivesdk

## 📝 Changelog
- 2026-11-10 18:05 — iOS added, unified hub, same otter/logic, FamilyControls shield
- 2026-11-10 14:55 — Android scaffold
- 2026-11-10 14:50 — inception

## 🔗 Quick Links
- Hub: https://drive.google.com/drive/folders/1q-gWovIsOkV1cqrfH-rip1DwpP9OhH4T
- **ONE LINK TO PASTE:** https://drive.google.com/file/d/1yITUZ_Iq4g4tf_3a3Gv4dAi0uoAaVDjO/view?usp=drivesdk (this file) — also v2: https://drive.google.com/file/d/1DpxAnw2ZblxOz8-_mtTYUW56xL8QSr-k/view?usp=drivesdk
- See v2 file for full iOS toolchain details.
