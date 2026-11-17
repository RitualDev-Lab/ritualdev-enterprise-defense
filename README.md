# RitualDev Enterprise Defense Gate (`ritualdev-enterprise-defense`)

[![CI](https://github.com/RitualDev-Lab/ritualdev-enterprise-defense/actions/workflows/ci.yml/badge.svg)](https://github.com/RitualDev-Lab/ritualdev-enterprise-defense/actions)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Secured by AgentShield](https://ritualdev.in/badges/secured-by-agentshield.svg)](https://ritualdev.in)

> Turnkey, single-action enterprise security gate for GitHub Actions. Runs AgentShield sandboxed execution, WebSecAuditor AST audits, SARIF GitHub Code Scanning upload, and executive HTML security report archiving.

---

## ⚡ Quickstart

Drop this job into your `.github/workflows/ci.yml`:

```yaml
name: "CI & Security Gate"

on:
  pull_request:
    branches: [main, master]
  push:
    branches: [main, master]

permissions:
  contents: read
  pull-requests: write
  security-events: write
  actions: read

jobs:
  defense-gate:
    name: "RitualDev Enterprise Defense"
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - uses: actions/setup-node@v4
        with:
          node-version: 22

      - name: "Run Enterprise Defense Gate"
        uses: RitualDev-Lab/ritualdev-enterprise-defense@v1
        with:
          test-command: "npm test"
          profile: "strict"
          network-policy: "allow-git-only"
          fail-on-severity: "HIGH"
          upload-sarif: "true"
          archive-report: "true"
```

---

## 🛡️ Core Capabilities

| Capability | Component | Description |
| :--- | :--- | :--- |
| **Sandboxed Execution** | `@ritualdev-lab/agentshield` | Confines test processes inside Bubblewrap/Seatbelt/LowBox containers with zero-leak egress. |
| **AST Security Audit** | `@ritualdev-lab/web-sec-auditor` | Inter-procedural static AST taint analysis detecting prompt injections, API keys, and unsafe sinks. |
| **GitHub Code Scanning** | `OASIS SARIF v2.1.0` | Native ingestion into GitHub Security tab with 1-click remediation diffs. |
| **Executive Reports** | HTML Audit Dossier | Downloadable single-file executive compliance report ready for SOC 2 and ISO 27001 auditors. |
| **Strict Air-Gapping** | `AGENTSHIELD_AIR_GAPPED=1` | Blocks all outbound telemetry; 100% offline analysis. |

---

## 📋 Inputs

| Input | Description | Default |
| :--- | :--- | :--- |
| `test-command` | Test command to execute inside sandboxed container | `npm test` |
| `profile` | AgentShield isolation profile (`strict`, `balanced`, `monitor`) | `strict` |
| `network-policy` | Egress network rule (`allow-git-only`, `loopback-only`, `air-gapped`) | `allow-git-only` |
| `sarif-file` | Target path for SARIF v2.1.0 report | `results.sarif` |
| `html-report` | Target path for HTML executive report | `report.html` |
| `fail-on-severity` | Severity threshold to fail build (`CRITICAL`, `HIGH`, `MEDIUM`, `LOW`, `NEVER`) | `HIGH` |
| `upload-sarif` | Whether to upload SARIF to GitHub Code Scanning | `true` |
| `archive-report` | Whether to upload HTML report as workflow artifact | `true` |
| `air-gapped` | Force 100% offline air-gapped zero outbound telemetry | `true` |

---

## 📄 License

Apache-2.0 © [RitualDev Lab](https://ritualdev.in).

---

## 🛡️ Community & Governance
- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing Guidelines](CONTRIBUTING.md)
- [Security Policy](SECURITY.md)
- [Accessibility Statement](ACCESSIBILITY.md)
- [License](LICENSE)
