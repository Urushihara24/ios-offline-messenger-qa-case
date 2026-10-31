# QA Report — iOS Offline Messenger Simulator

## Executive summary

A development-signed local/offline messenger simulator was tested on a physical iPhone 13 running iOS 18.2.

The mandatory acceptance scope completed with **8 of 9 checks fully passing**. The only direct acceptance failure was partial text selection: the message context menu opens, but standard iOS selection handles are unavailable.

Exploratory testing found four additional defects, including a deterministic crash when opening a fully empty correspondent profile.

## Execution summary

| Metric | Result |
|---|---:|
| Total test cases | 61 |
| PASS | 40 |
| FAIL | 5 |
| NOT RUN | 16 |
| BLOCKED | 0 |

The 16 `NOT RUN` cases are expanded boundary/negative/backup scenarios outside the mandatory acceptance scope. They are retained to show planned coverage rather than being falsely marked as executed.

## Mandatory acceptance result

| # | Check | Result | Notes |
|---|---|---|---|
| 1 | Chat list | PASS | Avatar, name, preview, time and unread counter verified |
| 2 | Chat history | PASS | Dates/times plus one/two outgoing checkmarks verified |
| 3 | Correspondent status | PASS | Online, recently seen and animated typing verified |
| 4 | Send text message | PASS | Input clears and outgoing message appears |
| 5 | Correspondent profile | PASS | Required profile fields verified |
| 6 | Context menu + text selection | FAIL | Context menu works; partial text selection does not |
| 7 | Settings / own profile | PASS | Settings tab and own profile presentation verified |
| 8 | Chat wallpapers | PASS | Change and reset verified |
| 9 | Persistence | PASS | Messages and wallpaper survive full restart |

## Optional hidden editor

The editor opens through the expected long-press gesture and supports creation/modification of local correspondents, chats, messages, timestamps, checkmarks and statuses.

Persistence of editor changes was verified.

A separate defect affects **editing the already-created own profile**: save operations for own name, birth date and avatar remain on an endless loader.

## Exploratory findings

Verified behavior included:

- multiple correspondents and chats remain isolated;
- edited/deleted data persists after restart;
- cancelling an edit keeps the previous value;
- rapid repeated actions do not create obvious duplicate entities;
- empty and whitespace-only messages are not sent;
- emoji-only, multiline and 1000-character messages render without breaking the UI;
- long profile values remain displayable;
- avatars can be changed;
- local functionality works without network access;
- the simulator coexists with the real Telegram application and does not expose its local data.

## Defects

See [BUG_REPORTS.md](../bugs/BUG_REPORTS.md).

The most important findings are:

1. **BUG-01 — acceptance failure:** partial text selection unavailable.
2. **BUG-05 — stability failure:** reproducible crash on fully empty correspondent profile.
3. **BUG-04 — optional-editor failure:** own-profile editing never completes.

## Crash evidence

BUG-05 was reproduced twice. Both captured `.ips` reports matched on exception/signal, faulting thread and application frame sequence.

No unsupported root-cause statement was added because symbolication with the matching dSYM was unavailable.

See [CRASH_ANALYSIS.md](CRASH_ANALYSIS.md).

## Final assessment

Build 17 is suitable for demonstrating the main local messenger flow: startup is stable, core chat interaction works, local data persists and test data remains isolated from the real Telegram application.

For final product acceptance, the direct acceptance failure in BUG-01 and the deterministic crash in BUG-05 should be fixed and retested. BUG-04 should also be resolved if the hidden editor is expected to be used by operators after initial data creation.
