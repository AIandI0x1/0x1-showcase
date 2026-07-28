# 0x1 — Orchestra Unified

> **AI-governed work orchestration platform.** Private source, public showcase.

## What it is

0x1 is a system for orchestrating AI agents across local and cloud infrastructure —
managing their work, verifying their output, and maintaining a tamper-evident audit
trail of every action taken. Think of it as a project management and governance
system for AI-driven work.

The platform introduces **AI-governed work**: every task an agent performs is
tracked, evidence-verified, and chained to a tamper-evident audit log. Work can
be validated, reviewed, and integrated — or rejected and repaired — without human
intervention at every step.

## By the numbers

| Metric | Value |
|---|---|
| Python modules | 6,400+ |
| Git commits | 14,310 |
| Test files | 1,359 |
| Chain blocks (hash-linked) | 475 |
| Total events (audit log) | ~299,000 |
| Active events (current chain) | 49,823 |
| Compacted events (checkpointed) | 249,351 |
| Development goals managed | 201 |
| Tasks tracked | 3,383 |
| Integrated goals | 181 |
| Audit problems | 0 |

All work is done on local hardware (AMD Strix Halo, 128 GB unified memory) with
multi-node synchronisation over Tailscale (macOS + Linux).

## Architecture overview

```
┌─────────────────────────────────────────────────────────┐
│                    0x1 Runtime                           │
├──────────────┬──────────────┬───────────────────────────┤
│  CLI Pipeline │  State Store │  Hash-Chain Audit Log     │
│  (ou_cli.py)  │  (main.json) │  (events.ndjson + blocks) │
├──────────────┴──────────────┴───────────────────────────┤
│              Agent Orchestration Layer                    │
│  ┌─────────┐ ┌─────────┐ ┌──────────┐ ┌──────────┐      │
│  │ Thalamus│ │Hippocamp│ │  Cortex  │ │ Basal-G  │      │
│  │ (router)│ │ (memory)│ │ (compute)│ │ (reward) │      │
│  └─────────┘ └─────────┘ └──────────┘ └──────────┘      │
├───────────────────────────────────────────────────────────┤
│           Local LLM Inference (llama-gateway)             │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐    │
│  │ qwen3.6-35b  │  │  qwen3:4b    │  │  vision (VL) │    │
│  │  (8080)      │  │  (8081)      │  │  (8082)      │    │
│  └──────────────┘  └──────────────┘  └──────────────┘    │
├───────────────────────────────────────────────────────────┤
│        Multi-Node Sync (Tailscale, macOS + Linux)         │
└───────────────────────────────────────────────────────────┘
```

## Key subsystems

### Task lifecycle with evidence verification

Every task follows a canonical lifecycle: **activate → implement → evidence →
validate (audit + make check + make test) → closeout → integrate.** No task is
marked complete until it passes all validation gates. Evidence is verified
against the actual repo state — fabricated evidence is detected and rejected.

### Hash-chain audit log

All state mutations are recorded as events in an append-only log
(`events.ndjson`). Events are hash-chained: each event references the SHA-256 of
the previous event. Events are sealed into checkpoint blocks (475 blocks,
~299K events total). The chain is self-healing — drift is detected and repaired
automatically.

### Canonical state

A single JSON file (`main.json`) is the source of truth for all goals, tasks,
and system state. State mutations go through CLI mutators only — no hand-editing.
Every mutation produces an event in the audit log.

### Synthetic brain architecture

Process distribution is modelled on brain anatomy: the **thalamus** routes
events, the **hippocampus** stores long-term memory, the **cortex** handles
compute, the **basal ganglia** manages reward/feedback loops. Each region is a
container with defined inputs, outputs, and boundaries.

### Local LLM inference

Models run on AMD Strix Halo (128 GB unified memory) via `llama-gateway`:
- qwen3.6-35b-a3b (primary, 2 parallel slots, ~22 GB)
- qwen3:4b (secondary, 4 parallel slots, ~3 GB)
- Vision model for screenshot/image analysis

The system orchestrates work across cloud and local models — cloud for
orchestration and dispatch, local for execution. The local execution layer is
being bootstrapped now, with the goal of 100% local responsibility.

## Technologies

- **Language:** Python (6,400+ modules)
- **State:** JSON + hash-chain (custom implementation)
- **Inference:** llama.cpp / llama-server, ROCm, MCP protocol
- **Network:** Tailscale (multi-node sync)
- **Hardware:** AMD Strix Halo (Radeon 8060S, 128 GB unified memory)
- **CI:** Makefile-based pipeline (`make check`, `make test`, tiered checks)

## Repository access

The source code is private. Access is available on request for:
- Potential employers and internship reviewers
- Commercial partners and clients
- Collaborators

Contact: andre.hamm1@gmx.de

## License

Proprietary. All rights reserved.
