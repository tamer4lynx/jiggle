# Jiggle native module (iOS + Android)

Vibration/haptic native module for Lynx. Exposes `vibrate(durationMs)` to the Lynx runtime.

## Installation

```bash
npm i @tamer4lynx/jiggle@prerelease
```

Add to your app's dependencies and run `t4l link`.

## API

| Method | Description |
|--------|-------------|
| `vibrate(durationMs)` | Vibrates the device for the provided duration in milliseconds |

**Parameters:** `durationMs` (number) — duration in milliseconds.

**Usage (example):**

```js
if (global.NativeModules?.Jiggle) {
  NativeModules.Jiggle.vibrate(200)
}
```

## Layout

- `android/` — Android module (Gradle + Kotlin). Main class: `JiggleModule.kt` (uses Vibrator/VibratorManager).
- `ios/jiggle/` — CocoaPods podspec and Swift source. Uses CoreHaptics with AudioToolbox fallback.

## Configuration: lynx.ext.json

This package uses **lynx.ext.json** (RFC standard). Example:

```json
{
  "platforms": {
    "android": {
      "packageName": "com.nanofuxion.vibration",
      "moduleClassName": "com.nanofuxion.vibration.JiggleModule",
      "sourceDir": "android"
    },
    "ios": {
      "podspecPath": "ios/jiggle",
      "moduleClassName": "JiggleModule"
    }
  }
}
```

From the repo root:

```bash
t4l link --both
```

## Development

- iOS: `pod lib lint packages/jiggle/ios/jiggle.podspec`
- Android: build with Gradle from `packages/jiggle/android`.
