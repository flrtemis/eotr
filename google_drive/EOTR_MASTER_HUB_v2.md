# 🦦 EOTR — MASTER HUB (Single Link Bootstrap) — v2 with iOS
### Eye's On The Road — pronounced "otter"
**This is the ONE link to paste at the start of any new chat with Arena.**

> When I paste this file's Google Drive link in a new chat, you (the assistant) must: 1) read THIS file fully, 2) list files in the shared hub folder, 3) read the latest project zips (Android + iOS), and 4) continue from where we left off — no re-asking about machines/tools/objective.

## 🤖 INSTRUCTIONS FOR FUTURE ASSISTANT (READ FIRST)

1. Fetch hub folder `eotr — Eye's On The Road (Shared Build Hub)` — list contents. Source of truth is Drive.
2. Treat tools below as canonical — we both use same exact tools to build same exact apps (Android = APK, iOS = IPA). If user hits snag, suggest same toolchain.
3. Never ask again for: 10s rule, otter icon, package name, thresholds — it's here.

---

## 📌 Project Identity

- **Name:** eotr (otter) / Full: Eye's On The Road
- **Bundle ID (both):** `com.eotr.eyesontheroad` (Android package, iOS bundle)
- **Version:** `1.0.0-otter` for both
- **Mascot:** otter floating on back holding phone — `ic_otter_mascot.png` shared
- **Location:** New Castle, DE

## 🎯 Objective

> Leverage accelerometer + GPS + gyroscope to set persistent rule: screen only usable after 10,000 ms level & still. Otherwise shield/block. Prevent texting while driving.

Note: Original said "IF level & still" → implemented as **UNLESS** (lock when moving = life-saving). Applies to **both platforms**.

## 🔒 10,000 ms Rule — Canonical (SHARED — Android AND iOS)

All 4 true continuously 10s → UNLOCK/RELAX. Any fail → BLOCK/SHIELD.

| Signal | Threshold | Android code | iOS code |
|--------|-----------|--------------|----------|
| Accelerometer | `|mag-9.81|<0.9` & `var<0.35` | `StationaryDetector.kt` | `StationaryDetector.swift` |
| Gyroscope | `<0.12 rad/s` | `StationaryDetector.kt` | `StationaryDetector.swift` |
| GPS | `<0.5 m/s` & `<30m` accuracy | `DrivingDetectionService.kt` (FusedLocation) | `DrivingDetectionManager.swift` (CoreLocation) |
| Level | tilt `<15°` | `computeTiltDegrees()` | `tiltDegrees()` |

- Loop: 200 ms (5 Hz), GPS 1s, variance 20 samples — **same on both**
- Android enforcement: Foreground service + overlay + Accessibility + Boot + DeviceAdmin. iOS: CoreMotion loop + DeviceActivity + FamilyControls shield + ManagedSettingsStore. Both never block 911/SOS.

## 🛠️ Canonical Toolchains — WE BOTH USE SAME TOOLS

### Android (for APK)
- Kotlin 1.9.22, Java 17, Android Studio Hedgehog+, AGP 8.2.2, Gradle 8.6, compileSdk34/min26/target34
- Deps: play-services-location 21.2.0, core-ktx 1.12.0 etc.
- Output: `app/build/outputs/apk/debug/app-debug.apk`

### iOS (for IPA) — NEW
- Xcode 15+, Swift 5.9, SwiftUI, iOS 16.0+ (for FamilyControls)
- Sensors: CMMotionManager (accel 50Hz, gyro 50Hz), CLLocationManager (kCLLocationAccuracyBest, 1s)
- Blocking: FamilyControls + DeviceActivity + ManagedSettingsStore (shield apps) — only App-Store-allowed way. MDM for truly unbreakable (like Android Device Owner)
- Permissions: NSLocationAlways, NSMotionUsage, UIBackgroundModes location, FamilyControls entitlement
- Output: Xcode Archive → IPA (Ad Hoc/TestFlight)

### Shared Hub
- Drive folder: `eotr — Eye's On The Road (Shared Build Hub)` https://drive.google.com/drive/folders/1q-gWovIsOkV1cqrfH-rip1DwpP9OhH4T
- Icons: same otter PNG used as mipmap + Assets.xcassets AppIcon

## 💻 My Machines — FILL IN DRIVE

(See v1 file for template — edit directly in Drive. Add Mac specs for iOS + Windows for Android)

## 📂 Current Project State (2026-11-10 18:00 ET) — UPDATED FOR iOS

**Status:** ✅ Android scaffold complete (4.3 MB zip). ✅ iOS scaffold complete (411 KB zip). Both use same 10s logic, same thresholds. Both in hub.

**Hub contents now:**
- `EOTR_MASTER_HUB.md` — this bootstrap (1yITUZ...)
- `eotr-android-project.zip` — https://drive.google.com/file/d/1e8Q4JjMjHD0NrZOhNSNF7l167vL7nixU/view?usp=drivesdk
- `eotr-ios-project.zip` — https://drive.google.com/file/d/1CoJTDkVUqFxs6zcZXzbcW_xHzr3dijW9/view?usp=drivesdk — NEW
- `eotr-preview.html` — visual preview
- `EOTR_MASTER_HUB_v2.md` — this updated version (will replace v1 after you star it)

**iOS structure:**
```
eotr-ios/
├── Sources/eotrApp.swift, ContentView.swift, StationaryDetector.swift, DrivingDetectionManager.swift, BlockView.swift, ScreenTimeManager.swift
├── Resources/ic_otter_mascot.png (same otter)
├── README-iOS.md, BUILD_GUIDE-iOS.md, Info.plist.snippet.plist
```

**Key iOS decisions:**
- Ported StationaryDetector 1:1 from Kotlin to Swift — thresholds identical — no drift
- ScreenTimeManager no-ops gracefully if FamilyControls entitlement missing (eotr still warns inside app, but can't shield other apps — Apple's limit)
- interactiveDismissDisabled while blocking (like Android back-block)
- Background location via SignificantLocationChanges + allowsBackgroundLocationUpdates

**Key Android decisions (unchanged):**
- Unbreakable = best-effort; Device Owner for true enterprise

## 🔮 Plans

Now: Test Android APK locally, test iPhone flat 10s → green, move → red shield. Tune thresholds for I-95 bumps if needed.
Next v1.1: Add ActivityRecognition (Android) + CMMotionActivity (iOS) as 4th signal, dash-mount angle option
Future v2: Family fleet MDM (both platforms) — truly unbreakable for teen devices

## 📝 Changelog

- **2026-11-10 18:05 ET** — iOS version added — SwiftUI port, same 10s rule, FamilyControls shield, uploaded eotr-ios-project.zip. Hub now Android + iOS unified. Same otter, same logic. Comment added to Master Hub.
- **2026-11-10 14:55 ET** — Android scaffold + hub creation
- **2026-11-10 14:50 ET** — Inception

## 🔗 Quick Links (USE THESE)

- Hub: https://drive.google.com/drive/folders/1q-gWovIsOkV1cqrfH-rip1DwpP9OhH4T ⭐ STAR THIS
- **ONE LINK TO PASTE (bootstrap):** https://drive.google.com/file/d/1yITUZ_Iq4g4tf_3a3Gv4dAi0uoAaVDjO/view?usp=drivesdk
- Android zip: https://drive.google.com/file/d/1e8Q4JjMjHD0NrZOhNSNF7l167vL7nixU/view?usp=drivesdk
- iOS zip: https://drive.google.com/file/d/1CoJTDkVUqFxs6zcZXzbcW_xHzr3dijW9/view?usp=drivesdk
- Preview: https://drive.google.com/file/d/1WykdX_ioRYkVJPspXb0OX9MBdE7Yg0ei/view?usp=drivesdk

---
Edit me in Drive — update machines when you add Mac! Future us thanks us.
