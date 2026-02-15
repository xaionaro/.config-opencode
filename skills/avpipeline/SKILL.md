---
name: avpipeline
description: Architectural patterns and rules for the avpipeline project (portable libav wrapper).
triggers:
  - "avpipeline/**"
  - "avpipeline"
---

## Project Purpose

Provide a versatile, portable, high-level wrapper to simplify libav usage for building audio/video pipelines.

## Architecture

- **Kernel:** Performs actual packet or frame processing.
- **Processor:** Wraps a kernel; manages I/O and data flow control.
- **Node:** Wraps a processor; manages wiring between processors.
- **Pipeline:** A graph formed by multiple nodes.
- **Filters:** Used to filter connections between nodes.
- **Processing Modes:** Kernels can process incoming data or autonomously generate new packets/frames.

## Helpers

- **Router:** Publishes or consumes named streams.
- **Monitor:** Debugging feature to snoop on packets/frames.

## Rules

- **SEGFAULT:** A SEGFAULT is NEVER libav's fault. It is a bug in our code and MUST be fixed.
