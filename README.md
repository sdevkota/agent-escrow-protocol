# Agent Escrow Protocol

Human approval queues for costly, risky, or irreversible agent actions.

> Version: 1.0.0 | License: MIT | Status: production-oriented v1 foundation

## Problem

Agents need autonomy, but high-impact actions still require explainable intent, bounded authority, and auditable approval.

## What this project solves

An approval packet validator that checks action intent, risk class, budget, rollback plan, approver identity, and execution window.

Agent Escrow Protocol ships as a small, dependency-free CLI and library. It validates a domain-specific JSON packet, emits actionable findings, and gives contributors a concrete surface for adding adapters, richer checks, schemas, and integrations.

## Who it is for

Agent app developers, enterprise automation teams, governance engineers.

## Quick start

```bash
npm test
npm start -- sample
```

Analyze your own packet:

```bash
agent-escrow-protocol ./packet.json
```

Or pipe JSON:

```bash
cat packet.json | node src/cli.js
```

## Example packet

```json
{
  "action": {
    "kind": "deploy",
    "system": "production-api",
    "reversible": true
  },
  "risk": {
    "class": "high",
    "budgetUsd": 0
  },
  "approval": {
    "approver": "ops@example.org",
    "window": "2026-05-01T20:00Z"
  }
}
```

## Library usage

```js
const { analyze } = require("./src/index.js");

const report = analyze({
  "action": {
    "kind": "deploy",
    "system": "production-api",
    "reversible": true
  },
  "risk": {
    "class": "high",
    "budgetUsd": 0
  },
  "approval": {
    "approver": "ops@example.org",
    "window": "2026-05-01T20:00Z"
  }
});
console.log(report.summary);
```

## v1 behavior

- Validates required fields for the domain packet.
- Scores readiness from 0 to 100.
- Reports missing or weak governance evidence.
- Suggests next actions and contributor extension points.
- Runs fully offline with no API keys and no network access.

## Contribution map

Good first contributions:

- Add Slack approvals.
- Add signed approval receipts.
- Add rollback runners.
- Add policy packs.

Larger contributions:

- Add a JSON Schema and compatibility tests.
- Build import/export adapters for popular AI frameworks.
- Add real-world fixtures from public, non-sensitive examples.
- Improve scoring with transparent, documented heuristics.

## Project principles

- Human agency over blind automation.
- Open standards over vendor lock-in.
- Auditable decisions over hidden magic.
- Privacy and safety as design constraints, not release notes.

## GitHub Pages

The marketing site lives in `site/index.html`. Enable GitHub Pages from the `site` folder or use the included Pages workflow after publishing.

## Security

This project does not process secrets by default. If you build adapters that touch production systems, keep least privilege, explicit consent, and auditable logs in the design.
