# Evidence Policy

This public repository intentionally does **not** contain raw client screenshots, live syslog or `.ips` crash reports.

## Evidence captured in the original QA delivery

| Defect / check | Evidence type | Public handling |
|---|---|---|
| Context menu | Screenshot | Omitted from public repo |
| BUG-01 — text selection | Screenshot | Omitted from public repo |
| BUG-02 — destructive chat action | Screenshot | Omitted from public repo |
| BUG-05 — empty-profile crash | Live syslog | Sanitized findings documented in `CRASH_ANALYSIS.md` |
| BUG-05 — empty-profile crash | Crash report #1 (`.ips`) | Raw file omitted |
| BUG-05 — empty-profile crash | Crash report #2 (`.ips`) | Raw file omitted |

## Why raw artifacts are excluded

Real-device artifacts can contain information that is unnecessary for a public portfolio:

- local filesystem/container paths;
- signing/team identifiers;
- device/runtime identifiers;
- client-created profile/message data;
- timestamps and other environment metadata.

Publishing those files would add privacy and confidentiality risk without materially improving the portfolio case.

## What is preserved publicly

The repository retains the information needed to evaluate the QA work:

- test scenario and status;
- defect reproduction steps;
- Expected vs Actual;
- Severity / Priority;
- test-case ↔ defect traceability;
- reproducibility;
- exception/signal and faulting-thread data;
- crash-signature comparison;
- explicit statement of what cannot be concluded without dSYM symbolication.

See [Crash Analysis](../docs/CRASH_ANALYSIS.md) for the sanitized technical evidence.
