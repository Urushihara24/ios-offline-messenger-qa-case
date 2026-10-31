# Evidence Index & Publication Policy

This public repository intentionally excludes raw client screenshots, live syslog, and native `.ips` crash reports.

The original QA delivery contained the evidence required for defect reproduction and developer handoff. The public portfolio version preserves the evidence map and technical conclusions without exposing sensitive runtime data.

## Evidence index

| Defect / check | Evidence type | Original delivery | Public handling |
|---|---|---|---|
| Context-menu verification | Screenshot | Included | Raw image omitted |
| BUG-01 — text selection | Screenshot | Included | Raw image omitted; behavior documented |
| BUG-02 — destructive chat action | Screenshot | Included | Raw image omitted; behavior documented |
| BUG-03 — reply context | Execution record | Included in test run | No separate public screenshot |
| BUG-04 — own-profile loader | Execution record | Included in test run | No separate public screenshot |
| BUG-05 — empty-profile crash | Live syslog | Included | Raw log omitted; sanitized findings published |
| BUG-05 — empty-profile crash | Crash report #1 (`.ips`) | Included | Raw file omitted |
| BUG-05 — empty-profile crash | Crash report #2 (`.ips`) | Included | Raw file omitted |

## Why raw artifacts are excluded

Real-device evidence can contain information that is unnecessary for a public portfolio:

- local filesystem and application-container paths;
- signing/team identifiers;
- device/runtime identifiers;
- client-created profile or message data;
- precise timestamps and environment metadata;
- other runtime details unrelated to evaluating the QA work.

Publishing those files would add confidentiality risk without materially improving the portfolio case.

## What is preserved publicly

The repository retains the information needed to evaluate the QA work:

- test scenario and execution status;
- reproduction steps;
- Actual vs Expected;
- Severity / Priority;
- test-case ↔ defect traceability;
- reproducibility;
- evidence type;
- exception/signal and faulting-thread data for BUG-05;
- crash-signature comparison;
- explicit statement of what cannot be concluded without dSYM symbolication.

## Crash evidence chain

For BUG-05, the private evidence chain was:

```text
controlled reproduction
        ↓
live syslog capture
        ↓
2 native .ips reports
        ↓
matching exception / thread / frame sequence
        ↓
stable reproducible crash signature
```

See [Crash Analysis](../docs/CRASH_ANALYSIS.md) for the sanitized technical investigation.

## Portfolio rule

The public repository documents **how the conclusion was reached** without pretending that private raw evidence is safe or necessary to publish.
