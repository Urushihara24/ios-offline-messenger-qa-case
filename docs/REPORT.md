# Final QA Report — iOS Offline Messenger

## Executive summary

Build 17 of a local/offline iOS messenger simulator was tested on a physical iPhone 13 running iOS 18.2.

The mandatory acceptance scope finished with **8 of 9 checks fully passing**. The only direct acceptance failure was message-text selection: the long-press context menu works, but standard partial-selection handles are unavailable.

Exploratory testing identified four additional defects, including a deterministic crash when opening a fully empty correspondent profile.

## Execution snapshot

| Metric | Result |
|---|---:|
| Total test cases | 61 |
| PASS | 40 |
| FAIL | 5 |
| NOT RUN | 16 |
| BLOCKED | 0 |
| Mandatory acceptance | 8 / 9 fully passed |

The 16 `NOT RUN` cases are expanded boundary, backup, permission, or timing scenarios outside the mandatory acceptance run. They remain visible to preserve execution honesty and planned coverage.

## Mandatory acceptance result

| # | Check | Result | Notes |
|---|---|---|---|
| 1 | Chat list | PASS | Avatar, name, preview, time, unread counter verified |
| 2 | Chat history | PASS | Dates/times plus one/two outgoing checkmarks verified |
| 3 | Correspondent status | PASS | Online, recently seen, animated typing verified |
| 4 | Send text message | PASS | Input clears; outgoing message appears |
| 5 | Correspondent profile | PASS | Required profile fields verified |
| 6 | Context menu + text selection | FAIL | Context menu works; partial text selection does not |
| 7 | Settings / own profile | PASS | Settings tab and own profile presentation verified |
| 8 | Chat wallpapers | PASS | Change and reset verified |
| 9 | Persistence | PASS | Messages and wallpaper survive full restart |

## Exploratory and regression coverage

Verified behavior included:

- multiple correspondents and chats remain isolated;
- edited and deleted local data persists after restart;
- cancelling an edit keeps the previous value;
- rapid repeated actions do not create obvious duplicate entities;
- empty and whitespace-only messages are not sent;
- emoji-only, multiline, and 1000-character messages render without breaking the UI;
- long profile values remain displayable;
- avatars can be changed;
- local functionality remains available without network access;
- the test build coexists with the real Telegram application and does not expose its local data;
- repeated cold starts of build 17 remain stable after startup crashes observed in an earlier build.

## Optional hidden editor

The hidden editor opens through the expected long-press gesture and supports creation/modification of local correspondents, chats, messages, timestamps, checkmarks, statuses, and unread values.

Persistence of editor changes was verified.

A separate defect affects **editing the already-created own profile**: save operations for own name, birth date, and avatar remain on an endless loader.

## Defect summary

| ID | Severity | Priority | Summary |
|---|---|---|---|
| BUG-01 | Medium | P1 | Partial message-text selection is unavailable |
| BUG-02 | Medium | P2 | Whole-chat delete is exposed from single-message context |
| BUG-03 | Medium | P2 | Reply loses source-message context |
| BUG-04 | Medium | P1 | Own-profile editing hangs on endless loader |
| BUG-05 | High | P1 | Fully empty correspondent profile causes a crash |

Detailed reports: [BUG_REPORTS.md](../bugs/BUG_REPORTS.md).

## Crash investigation

BUG-05 was reproduced **2 / 2** times under controlled conditions. Both captured `.ips` reports matched on:

- `EXC_BREAKPOINT` / `SIGTRAP`;
- faulting thread `0`;
- the same top application framework;
- the same application-frame sequence and offsets.

The evidence supports a stable crash signature. It does **not** support an exact source-level root cause without matching dSYM symbolication.

Detailed analysis: [CRASH_ANALYSIS.md](CRASH_ANALYSIS.md).

## Release-readiness assessment

Build 17 is suitable for demonstrating the main local messenger flow: launch is stable, core chat interaction works, local data persists, offline behavior is functional, and the simulator remains isolated from the real Telegram application.

Before final product acceptance:

1. **BUG-05** should be fixed and retested because it is a deterministic application crash.
2. **BUG-01** should be fixed because it directly violates the mandatory acceptance criteria.
3. **BUG-04** should be resolved if operators are expected to edit the own profile after initial setup.
4. BUG-02 and BUG-03 should be reviewed as secondary interaction/UX defects.

## Delivery note

The original QA delivery included structured test execution, defect reports, screenshots, live syslog, and two `.ips` crash reports. This public repository is sanitized and intentionally excludes client-identifying or runtime-sensitive raw artifacts.
