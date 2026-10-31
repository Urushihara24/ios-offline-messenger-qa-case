# iOS Offline Messenger Simulator — QA Case Study

> Sanitized real-device QA case covering acceptance testing, exploratory testing, persistence, offline behavior, data isolation, hidden-editor workflows, and reproducible iOS crash analysis.

<p align="center">
  <img src="https://img.shields.io/badge/iOS-18.2-black?style=for-the-badge&logo=apple&logoColor=white" alt="iOS 18.2">
  <img src="https://img.shields.io/badge/Real_Device-iPhone_13-555555?style=for-the-badge" alt="iPhone 13">
  <img src="https://img.shields.io/badge/Manual_QA-Acceptance_%2B_Exploratory-6E40C9?style=for-the-badge" alt="Manual QA">
  <img src="https://img.shields.io/badge/Crash_Analysis-.ips_%2B_syslog-0A84FF?style=for-the-badge" alt="Crash analysis">
</p>

> **Disclaimer:** this repository documents testing of an unofficial local/offline messenger simulator with a Telegram-like UI. It is not affiliated with, endorsed by, or distributed by Telegram. Product data and runtime evidence have been sanitized for public portfolio use.

## Result at a glance

| Metric | Result |
|---|---:|
| Test cases | 61 |
| PASS | 40 |
| FAIL | 5 |
| NOT RUN | 16 |
| BLOCKED | 0 |
| Mandatory acceptance checks | 8 / 9 passed fully |
| Confirmed defects | 5 |
| Reproducible crash | 2 / 2 identical signatures |

**Start here:** [QA report](docs/REPORT.md) · [test cases](test_cases/TEST_CASES.md) · [bug reports](bugs/BUG_REPORTS.md) · [crash analysis](docs/CRASH_ANALYSIS.md) · [scope](docs/SCOPE.md)

## What was tested

The application is a local-only iOS messenger simulator. It does not require login, registration, server synchronization, or a real Telegram account. The acceptance scope covered:

- chat list UI: avatar, name, last-message preview, time, unread counter;
- chat history: dates, timestamps, outgoing-message checkmarks;
- correspondent states: online, recently seen, animated typing;
- sending local text messages;
- correspondent profile card;
- message context menu and text selection;
- settings and own profile presentation;
- chat wallpaper change/reset;
- persistence after force-close/relaunch;
- optional hidden service editor for profiles, chats, messages, timestamps, checkmarks and statuses.

## QA approach

1. Install and run a separately signed build on a physical iPhone.
2. Confirm that the test build coexists with the real Telegram app and cannot see its data.
3. Execute mandatory acceptance checks first.
4. Extend coverage with exploratory, negative, boundary, persistence and offline checks.
5. Link failed scenarios to concrete defect IDs.
6. For the crash defect, reproduce twice, collect live syslog and `.ips` reports, compare signatures and identify the top faulting framework.
7. Keep raw crash artifacts private; publish only sanitized technical findings.

## Key engineering finding

The strongest defect was a deterministic crash when opening a correspondent profile after all profile data had been removed through the service editor.

Two independent crash reports from the same build produced the same signature:

```text
Exception: EXC_BREAKPOINT
Signal: SIGTRAP
Faulting thread: 0
Top application image: TelegramUIFramework
Reproduction: 2 / 2
Signature match: identical
```

Exact source-level attribution was intentionally not claimed because the matching dSYM was not available. See [CRASH_ANALYSIS.md](docs/CRASH_ANALYSIS.md).

## Repository structure

```text
.
├── README.md
├── bugs/
│   └── BUG_REPORTS.md
├── docs/
│   ├── CRASH_ANALYSIS.md
│   ├── LEGEND.md
│   ├── REPORT.md
│   ├── SCOPE.md
│   └── TEST_ENVIRONMENT.md
├── evidence/
│   └── README.md
└── test_cases/
    └── TEST_CASES.md
```

## Public evidence policy

Screenshots, raw syslog and `.ips` crash files are not published because they may contain client data, local identifiers or runtime metadata. The repository keeps sanitized observations, reproduction steps, crash signatures and artifact mapping instead.

---

## More QA & engineering work

[🌐 Portfolio](https://vsevolodqa.ru/) · [💬 Telegram](https://t.me/vsevolod_qa) · [GitHub profile](https://github.com/Urushihara24)
