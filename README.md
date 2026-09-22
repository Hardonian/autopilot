# autopilot

Unified runnerless autopilot platform: ops, finops, growth, and support automation.

## Monorepo Structure

```
autopilot/
├── ops/        — Runnerless reliability autopilot (events → anomalies → diagnoses → JobForge requests)
├── finops/     — Runnerless FinOps autopilot (billing reconciliation, anomaly detection, churn risk)
├── growth/     — Runnerless growth/SEO autopilot (site audits, experiments, content drafts)
├── support/    — Runnerless support autopilot (ticket triage, cited replies, KB patches)
└── package.json / pnpm-workspace.yaml
```

## Modules

### [`ops/`](./ops/)
Consumes infrastructure events and manifests, detects anomalies, produces diagnoses and JobForge job requests. Includes contract definitions, profiles, and a CLI.

### [`finops/`](./finops/)
Reconciles billing data, detects cost anomalies, and surfaces churn-risk signals. Integrates with Stripe and SaaS metrics.

### [`growth/`](./growth/)
Scans site structure for SEO issues, proposes experiments, and drafts content — never auto-publishes.

### [`support/`](./support/)
Triages incoming support tickets, drafts cited responses, and proposes knowledge-base patches.

## Getting Started

Each module is self-contained with its own `package.json`, build scripts, and tests. Install and build independently:

```bash
# Example: build ops
cd ops
pnpm install
pnpm build
pnpm test
```

Or install all at once from the root:

```bash
pnpm install --recursive
pnpm --recursive build
pnpm --recursive test
```

## Tech Stack

- **Language:** TypeScript (ESM)
- **Build:** tsup / tsc
- **Test:** Vitest
- **Package Manager:** pnpm (>= 9)
- **Runtime:** Node.js >= 20

## License

Each module carries its own license. See individual `LICENSE` files for details.
