# 0x1 — Orchestra Unified

> **AI-governed work orchestration platform.** Private source, public showcase.

## Modules

0x1 is the main project, with components absorbed from other repositories:

- **Agent harness** — hermes-agent (local and cloud agent execution)
- **Communication platform** — buzz (hive-mind communication)

### Hardware ports (AMD Strix Halo, gfx1151)

Inference optimization tools ported to AMD Strix Halo (RDNA 3.5), with
documented evidence. Forks on this profile, branch `port/strix-halo-gfx1151`:

| Project | What was done |
|---|---|
| **Hyperloom** | GPU type detection for gfx1151, llama.cpp framework adapter, 135 tests passing |
| **Magpie** | Benchmark scripts for Strix Halo, TraceLens validation, hardware-agnostic trace analysis |
| **GEAK** | RDNA 3.5 hardware knowledge, Triton and HIP kernel verification, wave32/wave64 guidance |

All three hardware-verified on device: `_autodetect_gpu_type() = 'strix-halo'`

### Upstream PR contributions

- **[hermes-agent #6776](https://github.com/NousResearch/hermes-agent/pull/6776)** — fix for truncated streaming tool calls; cherry-picked into main with authorship preserved (225k★ project)
- **[SwiftLM #58](https://github.com/SharpAI/SwiftLM/pull/58)** — build.sh mlx-swift source path detection; merged
- **[buzz #2619](https://github.com/block/buzz/pull/2619)** — tenant-split bug in `normalize_host` across 3 components, incl. migration + tests; maintainer review: "P0 triage — merge candidate"

## Screenshots & Demo

### Dashboard — live graph visualization

![Dashboard](screenshots/dashboard-graph.jpeg)

The operator surface shows a live visualization of the system's internal graph:
2,372 nodes and 2,371 edges representing goals, tasks, insights, and plan nodes
across multiple layers. The left panel shows the task board workflow
(overview → active → doing → review → completed). The system renders
real-time projections of the canonical state.

### Canon Graph — interactive 3D demo (27 s)

[![Canon Graph — interactive 3D demo](screenshots/canon-graph-demo.gif)](https://github.com/AIandI0x1/0x1-showcase/raw/main/screenshots/canon-graph-demo.mp4)

Interactive walkthrough of the canon graph: rotation, zoom, and node
inspection — clicking a node opens the underlying goal record
(here: `G059`, type: goal, status: completed). The graph is a live
projection of the canonical state, not a mockup.

> The animation above plays inline; click it for the full-quality
> [MP4 (27 s, 1444×726)](https://github.com/AIandI0x1/0x1-showcase/raw/main/screenshots/canon-graph-demo.mp4).

> **Living system:** the video (2026-07-28) shows 2,247 nodes; the dashboard
> screenshot (2026-08) shows 2,372. The graph grows daily because it renders
> the actual state of work.

## What it is

0x1 is a system for orchestrating AI agents across cloud and local infrastructure —
managing their work, verifying their output, and maintaining a tamper-evident
audit trail of every action taken. Think of it as a project management and
governance system for AI-driven work.

The platform introduces **AI-governed work**: every task an agent performs is
tracked, evidence-verified, and chained to a tamper-evident audit log. Work can
be validated, reviewed, and integrated — or rejected and repaired — without human
intervention at every step.

## By the numbers

| Metric | Value (verified 2026-08-04) |
|---|---|
| Git commits | 24,758 |
| Python files | 9,156 |
| Functions (Python + Go) | 141,384 |
| Test files | 3,653 |
| CLI subcommands | 235 |
| Hash-chain blocks | 713 |
| Audit events (main chain) | ~300,000 (50,379 live + 249,351 sealed in checkpoints) |
| Audit events (all streams) | ~892,000 |
| Development goals managed | 205 |
| Tasks tracked | 3,382 |
| Audit problems | occasional |

## What it does

- **Agent orchestration** — dispatches work to AI agents across cloud and local
  infrastructure, tracks progress, and verifies results
- **Evidence-based verification** — every completed task must produce verifiable
  evidence; fabricated evidence is detected and rejected
- **Tamper-evident audit trail** — all state changes are hash-chained and
  sealed into checkpoint blocks, creating an immutable record of every action
- **Automated quality gates** — work passes through validation pipelines before
  it can be marked complete
- **Multi-node synchronisation** — runs across macOS and Linux nodes over a
  private mesh network

## Hardware

Local execution runs on AMD Strix Halo with 128 GB unified memory, supporting
parallel inference of large language models. The local execution layer is
currently being bootstrapped, with the goal of 100% local responsibility.

## Technologies

- **Language:** Python (9,100+ files), Go
- **Inference:** Local LLM inference via custom gateway
- **Audit:** Custom SHA256 hash chain (append-only, compaction checkpoints)
- **Network:** Multi-node sync over private mesh (Tailscale)
- **Hardware:** AMD Strix Halo (128 GB unified memory), Mac Mini M4 24GB Unified Memory, NVDA 3060 12GB plugged                   into mac mini using tinygrad

## Repository access

The source code is private. Access is available on request for:
- Potential employers and internship reviewers
- Commercial partners and clients
- Collaborators

## License

Proprietary. All rights reserved.
