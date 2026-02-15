---
name: wingout
description: Android control application for ffstream and associated automation scripts.
triggers:
  - "wingout/**"
  - "wingout"
---

## Project Purpose

Android-native application (WingOut) that serves as a UI/controller for the `ffstream` streaming engine via gRPC.

## Build System

- **Android Debug:** `scripts/build_android_debug.sh`.
  - Requires: `ANDROID_SDK_ROOT`, `ANDROID_NDK_ROOT`, and `QT_ANDROID_DIR` (e.g., `~/Qt/*/android_arm64_v8a`).
  - Uses CMake/Ninja for builds.
- **Desktop Debug:** `scripts/build_desktop_debug.sh`.
- **Artifacts:** Output APKs are typically placed in `build-android-debug/android-build/build/outputs/apk/debug/`.
