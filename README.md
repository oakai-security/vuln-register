# vuln-register

Dedicated, Git-backed vulnerability storage and risk acceptance register for the `@oakai-security` organization.

Part of the **Autonomous Vulnerability Remediation, Exception & Governance Pipeline** ([SPEC-020](file:///home/curt/dev/docs/specs/020-vulnerability-exception-and-remediation-governance.md)).

---

## Repository Structure

```
vuln-register/
├── register/
│   ├── vulnerability_register.md   # Living Markdown table of all CVEs and statuses
│   └── vulnerability_register.json # Machine-parseable JSON registry
├── tickets/
│   └── EXC-XXXX.md                 # Individual exception tickets with complete audit trail
└── README.md
```

---

## Governance Lifecycle & Ticket Format

Each exception request is filed under `tickets/EXC-XXXX.md` with structured frontmatter:

```yaml
---
id: EXC-0001
cve_id: CVE-2024-XXXX
package_name: libexample
installed_version: 1.0.0
host: lejeune
cvss_base: 7.5
epss_score: 0.008
in_memory: false
status: APPROVED
approved_by: vuln-exception-approver
approved_at: 2026-11-14T00:00:00Z
expires_at: 2026-12-14T00:00:00Z
sla_deadline: null
---
```

### Automation Worktrees
Micro-agents access this repository using isolated Git worktrees:
- `vuln-exception-requester`: Commits new `EXC-XXXX.md` tickets with status `PENDING_REVIEW`.
- `vuln-exception-approver`: Updates status to `APPROVED` or `REJECTED` and recalculates expiration / SLA deadlines.
