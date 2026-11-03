# 🛡️ nexHarden

[🇮🇷 فارسی](README.fa.md) | [🇬🇧 English](README.md)

**Linux Security Auditing & Hardening Framework**

nexHarden is a modular, safety-first toolkit for auditing Linux systems, identifying configuration weaknesses, generating professional reports, and applying carefully controlled hardening changes with full backup and rollback support.

> Configuration Compliance Score is an indicator only. A high score does **not** mean the system is secure.

## Features

- Read-only security auditing across 11 modules
- Transparent configuration compliance scoring
- Three hardening profiles: basic, standard, strict
- Dry-run by default; explicit approval required for changes
- Timestamped backups and verified rollback
- Self-contained HTML dashboard (no CDN, works offline)
- JSON reports for automation
- Local audit history
- Minimal dependencies (Python 3 standard library)

## Supported Platforms

Primary support:

| Distribution | Versions   | Architecture   |
|--------------|------------|----------------|
| Debian       | 12, 13     | x86_64, ARM64  |
| Ubuntu       | 22.04, 24.04 LTS | x86_64, ARM64 |

Other Debian/Ubuntu derivatives may work with warnings. Non-APT systems receive limited package checks.

## Requirements

- Python 3.9+
- Standard Linux utilities (`sysctl`, `ss`/`netstat`, `systemctl` on systemd systems)
- Root privileges only for privileged checks and hardening (audit works partially without root)

No mandatory pip packages.

## Installation

```bash
unzip nexHarden-1.0.0.zip
cd nexHarden
chmod +x nexharden harden.sh
```

Optional: place the directory on `PATH` or create a symlink.

## Quick Start

```bash
# System detection
./nexharden system-info

# Read-only audit (JSON + HTML reports)
./nexharden audit

# Full audit with all modules
sudo ./nexharden audit --full

# Specific module
./nexharden audit --module ssh

# Preview hardening (dry-run)
sudo ./nexharden harden --profile basic --dry-run

# Apply hardening (interactive confirmation)
sudo ./nexharden harden --profile basic --apply
```

Reports are written to `reports/`.

## CLI Commands

| Command | Description |
|---------|-------------|
| `audit` | Run security audit |
| `harden --profile NAME` | Preview or apply a profile |
| `backup list` | List hardening transactions |
| `rollback --transaction ID` | Restore a previous transaction |
| `history` | Show past audit summaries |
| `system-info` | Print detected system details |
| `version` | Print version |

### Audit options

- `--full` — include all modules
- `--module ssh,firewall` — run selected modules
- `--report html,json` — choose output formats

### Hardening options

- `--profile basic|standard|strict`
- `--dry-run` (default behavior when `--apply` is omitted)
- `--apply` — perform changes after confirmation
- `--yes` — skip interactive prompt (still creates backups; does not bypass SSH/firewall safety design)

## Audit Workflow

1. Detect distribution, kernel, firewall, SSH, privileges.
2. Execute selected modules (read-only).
3. Classify findings (PASS / FAIL / WARNING / UNKNOWN / N/A).
4. Compute weighted compliance score (UNKNOWN/N/A excluded).
5. Write JSON and HTML reports.
6. Store summary in local history.

## Hardening Workflow

1. Load profile and resolve inheritance.
2. Compare current values to targets.
3. Display dry-run plan.
4. On `--apply`, require explicit confirmation.
5. Create timestamped transaction backup.
6. Apply minimal changes (currently runtime sysctl).
7. Record results and transaction ID.
8. Re-audit recommended after changes.

**Important:** SSH and firewall rule changes are intentionally **not** auto-applied in 1.0.0. They are audited with recommendations only. Automatic modification of `sshd_config` or firewall policies requires additional recovery guarantees planned for future releases.

## Backup & Rollback

```bash
sudo ./nexharden backup list
sudo ./nexharden rollback --transaction TRANSACTION_ID
```

Rollback verifies that files still match the post-hardening state before restoring. Unexpected user modifications cause the restore to be refused.

## Project Structure

```
nexHarden/
├── nexharden          # CLI entry point
├── harden.sh          # Bash launcher
├── core/              # Engine, scoring, backup, reporter
├── modules/           # Audit modules
├── profiles/          # basic, standard, strict
├── dashboard/         # HTML/CSS/JS template
├── tests/             # Automated tests
├── reports/           # Generated reports
├── backups/           # Transaction backups
├── history/           # Audit history
└── docs/
```

## Scoring Formula

```
Score = (sum of weights of PASS checks) / (sum of weights of PASS + FAIL checks) × 100
```

Weights: CRITICAL=10, HIGH=5, MEDIUM=2, LOW=1. WARNING awards 0 points. UNKNOWN and N/A are excluded from the denominator.

## Limitations (1.0.0)

- Hardening currently applies **sysctl** settings only.
- SSH configuration and firewall rules are audited but not automatically modified.
- PAM changes are not applied automatically.
- Package upgrades are never performed by the tool.
- Desktop vs server heuristics are approximate.
- Not all kernel parameters exist on every kernel; missing ones are marked N/A.

## Security Warnings

- Always review dry-run output before applying.
- Keep an alternate access path when hardening remote systems.
- Reports must be treated as sensitive (file permissions 0600).
- This tool does not replace a full security assessment, intrusion detection, or patch management process.

## Troubleshooting

| Issue | Suggestion |
|-------|------------|
| `sshd -T` fails | Install `openssh-server` or run without SSH module |
| Incomplete user checks | Re-run with `sudo` |
| No HTML styling | Ensure `dashboard/` is present next to the CLI |
| Permission denied on reports | Check directory ownership |

## License

MIT License — see `LICENSE`.

## Version

1.0.0
