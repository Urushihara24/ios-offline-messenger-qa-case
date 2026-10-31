# iOS Offline Messenger — Commercial QA Project

> Commercial manual QA engagement covering real-device iOS acceptance testing, exploratory testing, offline/persistence behavior, application-data isolation, and reproducible crash investigation.

<p align="center">
  <img src="https://img.shields.io/badge/iOS-18.2-black?style=for-the-badge&logo=apple&logoColor=white" alt="iOS 18.2">
  <img src="https://img.shields.io/badge/Real_Device-iPhone_13-555555?style=for-the-badge&logo=apple&logoColor=white" alt="iPhone 13">
  <img src="https://img.shields.io/badge/Manual_QA-Acceptance_%2B_Exploratory-6E40C9?style=for-the-badge" alt="Manual QA">
  <img src="https://img.shields.io/badge/Crash_Analysis-.ips_%2B_syslog-0A84FF?style=for-the-badge" alt="Crash analysis">
</p>

| Scope | Evidence | QA focus |
|---|---|---|
| iOS messenger UI · local data · offline mode · hidden editor · persistence | Executed test cases · bug reports · screenshots · syslog · `.ips` crash reports | Acceptance · exploratory · negative/boundary checks · defect isolation · crash analysis |

**Start here:** [final report](docs/REPORT.md) · [test cases](test_cases/TEST_CASES.md) · [bug reports](bugs/BUG_REPORTS.md) · [crash analysis](docs/CRASH_ANALYSIS.md) · [evidence policy](evidence/README.md)

## Project profile

| Parameter | Value |
|---|---|
| Product | Local/offline iOS messenger simulator with a Telegram-like UI |
| Work type | Commercial manual mobile QA |
| Role | QA Engineer |
| Device | Physical iPhone 13 (`iPhone14,5`) |
| OS | iOS 18.2 |
| Application | 13.1.1, build 17 |
| Test focus | Acceptance, exploratory, persistence, offline, isolation, crash investigation |
| Test cycle | October 2026 |

The application uses a separate bundle and local data store. It does not require login, registration, backend synchronization, or access to a real Telegram account.

## Results in numbers

| Metric | Result |
|---|---:|
| Test cases | 61 |
| PASS | 40 |
| FAIL | 5 |
| NOT RUN | 16 |
| BLOCKED | 0 |
| Mandatory acceptance checks | 8 / 9 fully passed |
| Confirmed defects | 5 |
| Controlled crash reproductions | 2 / 2 |

The `NOT RUN` cases are retained deliberately: they are planned boundary, backup, permission, or timing checks that were not fully executed in this test cycle. They were not converted into synthetic PASS results.

## Key findings

1. **BUG-05 — High / P1:** opening a fully empty correspondent profile produces a deterministic application crash. Two independent `.ips` reports matched on exception, faulting thread, framework sequence, and frame offsets.
2. **BUG-01 — Medium / P1:** the required partial text-selection flow is unavailable because long press opens the context menu without standard iOS selection handles.
3. **BUG-04 — Medium / P1:** editing the already-created own profile does not complete; name, birth-date, and avatar changes remain on an endless loader.
4. **BUG-03 — Medium / P2:** the Reply action sends a normal message without preserving visible source-message context.
5. **BUG-02 — Medium / P2:** a whole-chat delete action is exposed from a single-message selection context, creating destructive-action ambiguity.

## QA approach

- installed and validated a separately signed build on a physical iPhone;
- verified coexistence and data isolation between the simulator and the real Telegram application;
- executed the nine mandatory acceptance checks first;
- expanded coverage with exploratory, negative, boundary, persistence, stability, and offline checks;
- linked failed test cases to concrete defect IDs;
- reproduced the crash twice under controlled conditions;
- captured live syslog and two `.ips` reports;
- compared crash signatures without claiming an unsupported source-level root cause;
- kept sensitive runtime artifacts private while preserving sanitized technical conclusions publicly.

## Crash investigation

The strongest technical finding was **BUG-05**. The failure was reproduced twice on the same build and device.

```text
Exception: EXC_BREAKPOINT
Signal: SIGTRAP
Faulting thread: 0
Top application image: TelegramUIFramework
Reproduction: 2 / 2
Signature match: identical
```

The crash was intentionally **not** attributed to a specific Swift function or source line because the matching dSYM was unavailable. Stable offsets establish a reproducible signature, not a defensible source-level cause.

[Read the crash analysis →](docs/CRASH_ANALYSIS.md)

## Documentation navigation

| Document | Purpose |
|---|---|
| [REPORT.md](docs/REPORT.md) | Final execution summary and release-readiness assessment |
| [SCOPE.md](docs/SCOPE.md) | Mandatory acceptance scope, exploratory extensions, exclusions |
| [TEST_ENVIRONMENT.md](docs/TEST_ENVIRONMENT.md) | Device, build, tooling, and regression context |
| [TEST_CASES.md](test_cases/TEST_CASES.md) | 61-case execution matrix with status and defect traceability |
| [BUG_REPORTS.md](bugs/BUG_REPORTS.md) | Full reports for BUG-01…BUG-05 |
| [CRASH_ANALYSIS.md](docs/CRASH_ANALYSIS.md) | Sanitized iOS crash investigation and handoff notes |
| [LEGEND.md](docs/LEGEND.md) | Status, severity, priority, and evidence conventions |
| [evidence/README.md](evidence/README.md) | Evidence index and public-publication policy |

## Confidentiality

This public repository is a sanitized portfolio version of the delivered QA work. It does not contain client-identifying profile/message data, raw device identifiers, signing-team information, raw syslog, or raw `.ips` files.

The product is an **unofficial Telegram-like local messenger simulator**. This repository is not affiliated with, endorsed by, or distributed by Telegram.

## Status

Documentation is frozen at the final build-17 QA result. The public case preserves the execution logic, defect traceability, and technical conclusions while omitting sensitive raw evidence.

---

## More QA & engineering work

[🌐 Portfolio](https://vsevolodqa.ru/) · [💬 Telegram](https://t.me/vsevolod_qa) · [GitHub profile](https://github.com/Urushihara24)
