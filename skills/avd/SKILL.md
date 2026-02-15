---
name: avd
description: Rules and operational procedures for AVD (Audio/Video daemon).
triggers:
  - "avd/**"
  - "avd"
---

## Project Purpose

Audio/Video daemon (AVD) acts as a receiver/processor for streams, often from `ffstream`.

## Environment & Configuration

- **Ports**:
  - `AVD_PORT_PUBLISHERS=1946`: For incoming streams (e.g., RTMP).
  - `AVD_PORT_CONSUMERS=1945`: For stream consumption.
- **Config Path**: Default `examples/ffstream-input.conf`.

## Debugging & Diagnosis

- **GDB Workflow**: `myscripts/run_avd_gdb.sh`.
  - Runs `avd` in batch mode.
  - Disables `SIGHUP` stop/print.
  - Captures full backtrace of all threads (`thread apply all bt full`).
  - Dumps registers and disassembled code (`disas /m`).
  - Output redirected to `gdb_output.log`.
