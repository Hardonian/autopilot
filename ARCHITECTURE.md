# autopilot — Architecture

> Part of the [Hardonia Platform](https://github.com/Hardonian/Hardonian).

## Position in the Platform

```
┌─────────────────────────────────────────────────────────────────┐
│                        HARDONIA PLATFORM                        │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐             │
│  │  AUTOPILOT   │  │ AGENT-INFRA │  │ AGENT-EDGE  │             │
│  │  ◄── THIS    │  │             │  │             │             │
│  │  ops/       │  │ control-    │  │ mesh-edge/  │             │
│  │  finops/    │  │  plane/     │  │ pcap/       │             │
│  │  growth/    │  │ mission-    │  │             │             │
│  │  support/   │  │  ledger/    │  └─────────────┘             │
│  │             │  │ agent-mesh/ │                               │
│  └──────┬──────┘  │ mcpwall/    │                               │
│         │         └──────┬──────┘                               │
│         │                │                                      │
│         └────────────────┤                                      │
│                    ┌─────▼─────┐                               │
│                    │ MODEL-    │                               │
│                    │ TOOLS     │                               │
│                    │ model-    │                               │
│                    │  forge/   │                               │
│                    │ inference-│                               │
│                    │  api/     │                               │
│                    │ ollama-   │                               │
│                    │  router/  │                               │
│                    └───────────┘                               │
├─────────────────────────────────────────────────────────────────┤
│  COMMERCIAL LAYER                                               │
│  hardonia-store · comfyui-workflow-packs · content-repo          │
└─────────────────────────────────────────────────────────────────┘
```

## What autopilot does

Runnerless automation across four domains — ops, finops, growth, and support.
Each module consumes platform events and produces actionable outputs (diagnoses,
cost anomalies, SEO drafts, support replies) without a persistent runner.

## Dependencies on sibling repos

| Dependency | Via | What it provides |
|---|---|---|
| [agent-infra](https://github.com/Hardonian/agent-infra) | control-plane | Execution of autopilot-generated job requests |
| [agent-infra](https://github.com/Hardonian/agent-infra) | mission-ledger | Cost tracking and governance for finops |
| [agent-infra](https://github.com/Hardonian/agent-infra) | mcpwall | Tool gating for support module |
| [model-tools](https://github.com/Hardonian/model-tools) | inference-api | LLM inference for content generation (growth) |

## Cross-repo data flow

```
autopilot/ops ──→ agent-infra/control-plane  (job requests)
autopilot/finops ──→ agent-infra/mission-ledger  (cost events)
autopilot/growth ──→ model-tools/inference-api  (content drafts)
autopilot/support ──→ agent-infra/mcpwall  (tool access policy)
```

## Sibling repos

- [agent-infra](https://github.com/Hardonian/agent-infra) — control-plane, mission-ledger, agent-mesh, mcpwall
- [agent-edge](https://github.com/Hardonian/agent-edge) — mesh-edge, pcap
- [model-tools](https://github.com/Hardonian/model-tools) — model-forge, inference-api, ollama-router
