---
name: ffstream
description: Operational, architectural, and environmental rules for the ffstream live streaming project.
triggers:
  - "ffstream/**"
  - "streamctl/**"
  - "mediamtx/**"
  - "ffstream"
---

## Project Goal

Provide portable, resilient live streaming (e.g., Android -> wireguard -> avd -> mpv).

- **Functionality:** Failover sensor consumption, bandwidth-aware compression, server streaming.
- **Tailoring:** `ffstream` and `avd` (Audio/Video daemon) are co-designed for dynamic changes (resolution, codecs).
- **Master Track:** Audio is the main track; stream ends when audio ends.

## System Architecture

- **Android:** Rooted (Magisk/userdebug), Termux installed.
- **Environment:** Ubuntu env in `/data/ubuntu` (auto-executed). `ffstream` runs in Termux for MediaCodec access.
- **UI:** WingOut app communicates via gRPC.

## Paths & Tools

- **Forbidden:** DO NOT edit or read `**/imports/**` or `**/import/**` (not source of truth).
- **SDK:** Android SDK is in `ffstream/.Android`.
- **Updates:** Check `ffmpeg/myscripts` for phone update procedures.
- **Container:** Dockerfile in `streamctl/docker/termux/Dockerfile`.

## Deployment & Production

- **Upload Prod:** `myscripts/upload-prod.sh`.
- **Upload Test:** `myscripts/upload-test.sh`.

## Test Environment

- **ADB:** Server at `192.168.0.159:5037`. Target phone at `192.168.0.159`.
- **Environment:** `LD_LIBRARY_PATH=/data/data/com.termux/files/home/lib`.
- **Manual Launch**: `ssh root@192.168.0.159 /usr/local/bin/run_ffstream.sh`.
- **Live Control:** `ffstreamctl --remote-addr tcp+ssl:192.168.0.159:3593 --help`.
- **Logging:** Default to `DEBUG`. `TRACE` only if necessary (performance impact).
- **Sleep Prevention:** Use `adb shell settings put system screen_off_timeout 2147483647` and `stay_on_while_plugged_in 7`.

## Test Scripts (`myscripts/`)

- `test-output-switch.sh`: Verifies output switching logic.
- `test-network-flap-phone.sh`: Simulates network instability for resilience testing.

Feel free to update or/and add scripts.

## Production Environment

- **gRPC:** Interface @ `172.29.170.2:3593`. Add debugging capabilities to gRPC if missing.
- **Logs:** `/tmp/mediamtx.log` via SSH (`root@172.29.170.2`). Android FS in `/android/`.
- **Policy:** Look only, DO NOT touch or restart production phones.
- **Launch Modes:** Launched via `mediamtx` (if evidence in log) or `/usr/local/bin/run-ffstream.sh`.

## Operational Rules

- **Production Confirmation:** Interactions with production (IP `172.29.170.2`, phone hardware) MUST be confirmed using the `question` tool.
- **Phone FS:** ONLY edit/modify files in Termux home or `ubuntu/tmp`.
- **Git:** Commit every change with a description to the `drafts` branch.
- **Cross-Repo:** If `avpipeline` changes, push to public as `drafts` and pull into `ffstream`.
- **SEGFAULT:** Our bug, MUST fix.
- **Performance:** No logs per frame unless level is `TRACE`.
