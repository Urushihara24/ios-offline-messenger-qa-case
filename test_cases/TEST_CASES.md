# Executed Test Cases — Build 17

## Execution snapshot

| Metric | Count |
|---|---:|
| Total | 61 |
| PASS | 40 |
| FAIL | 5 |
| NOT RUN | 16 |
| BLOCKED | 0 |

This is the sanitized execution matrix from the final QA run. Client-specific values and raw evidence are intentionally omitted, while execution status, observed result, and defect traceability are preserved.

`NOT RUN` means the scenario was planned but not fully executed in this test cycle; it is not treated as a synthetic PASS.

## Test execution

| ID | Area | Scenario | Priority | Type | Status | Result / note | Defect |
|---|---|---|---|---|---|---|---|
| IOS-001 | Launch | First application launch | P0 | Smoke | PASS | Build 17 launches and reaches chat list | — |
| IOS-002 | Chat list | Core row elements | P0 | Functional | PASS | Avatar, name, last-message preview and time visible | — |
| IOS-003 | Chat list | Unread counter | P1 | Functional/UI | PASS | Unread value displays, persists and resets after opening chat | — |
| IOS-004 | Chat list | Open chat from list | P0 | Smoke | PASS | Correct chat opens | — |
| IOS-005 | Chat | Message history | P0 | Functional/UI | PASS | Message order, dates and timestamps visible | — |
| IOS-006 | Chat | Single checkmark | P1 | Functional/UI | PASS | One checkmark renders correctly | — |
| IOS-007 | Chat | Double checkmark | P1 | Functional/UI | PASS | Two checkmarks render correctly | — |
| IOS-008 | Status | Online state | P1 | Functional/UI | PASS | Online state shown in header | — |
| IOS-009 | Status | Recently seen state | P1 | Functional/UI | PASS | Recently seen state shown correctly | — |
| IOS-010 | Status | Animated typing state | P1 | Functional/UI | PASS | Typing state and animation work | — |
| IOS-011 | Messaging | Send normal text | P0 | Functional | PASS | Input clears; outgoing message appears | — |
| IOS-012 | Messaging | Cyrillic + emoji | P1 | Functional/UI | PASS | Text renders without encoding/layout issues | — |
| IOS-013 | Messaging | Long multiline message | P1 | Boundary/UI | PASS | 1000-character/multiline text renders without layout break | — |
| IOS-014 | Messaging | Several messages in succession | P1 | Functional/Stability | PASS | No duplicate messages observed; UI responsive | — |
| IOS-015 | Profile | Open correspondent profile | P0 | Functional | PASS | Filled profile opens correctly | — |
| IOS-016 | Profile | Required profile fields | P0 | Functional/UI | PASS | Avatar, names, username, About and phone visible | — |
| IOS-017 | Message interaction | Long-press context menu | P0 | Functional | PASS | Context menu opens and app remains stable | — |
| IOS-018 | Message interaction | Partial text selection | P1 | Functional/iOS | FAIL | Long press opens menu; standard partial-selection handles unavailable | BUG-01 |
| IOS-019 | Navigation | Settings tab | P0 | Functional/UI | PASS | Final tab is settings with gear icon | — |
| IOS-020 | Settings | Own profile presentation | P1 | Functional/UI | PASS | Own photo/profile data visible | — |
| IOS-021 | Appearance | Open chat wallpaper settings | P0 | Functional | PASS | Wallpaper screen opens | — |
| IOS-022 | Appearance | Change chat wallpaper | P0 | Functional/UI | PASS | Selected wallpaper appears in chat | — |
| IOS-023 | Appearance | Reset wallpaper | P1 | Functional | PASS | Default wallpaper restored | — |
| IOS-024 | Persistence | Sent message after restart | P0 | Persistence | PASS | Sent message survives full restart | — |
| IOS-025 | Persistence | Wallpaper after restart | P0 | Persistence | PASS | Selected wallpaper survives full restart | — |
| IOS-026 | Stability | Background → foreground | P1 | Stability | PASS | App resumes without visible corruption/crash | — |
| IOS-027 | Stability | Repeated navigation | P1 | Stability | PASS | No duplicate screens or freezes observed | — |
| IOS-028 | Isolation | Test build coexists with real Telegram | P0 | Isolation | PASS | Both apps remain independently installed | — |
| IOS-029 | Isolation | No access to real Telegram data | P0 | Isolation | PASS | Real app chats/profile data are not visible in simulator | — |
| IOS-030 | Hidden editor | Open service editor | P2 | Optional | PASS | Long press in expected title area opens editor | — |
| IOS-031 | Hidden editor | Edit correspondent/profile data | P2 | Optional | PASS | Correspondent data updates correctly; own-profile issue tracked separately | BUG-04 note |
| IOS-032 | Hidden editor | Edit chats/messages | P2 | Optional | PASS | Changes appear in main UI | — |
| IOS-033 | Hidden editor | Edit dates/checkmarks/statuses | P2 | Optional | PASS | Edited values render correctly | — |
| IOS-034 | Hidden editor | Persist editor changes | P2 | Optional/Persistence | PASS | Editor changes survive restart | — |
| IOS-035 | Messaging | Empty message | P0 | Negative/Validation | PASS | Empty message is not created | — |
| IOS-036 | Messaging | Whitespace-only message | P1 | Negative/Validation | PASS | Visually empty message is not created | — |
| IOS-037 | Messaging | Exact one-character message | P1 | Boundary | NOT RUN | Exact 1-character boundary not executed separately | — |
| IOS-038 | Messaging | 255 / 256 / 1000 / 10000 boundaries | P1 | Boundary/Stability | NOT RUN | 1000 chars tested; full boundary matrix not executed | — |
| IOS-039 | Messaging | Emoji-only + full Unicode matrix | P1 | Boundary/Unicode | NOT RUN | Emoji-only verified; full ZWJ/modifier matrix not executed | — |
| IOS-040 | Chat list | Long name + long preview | P1 | Boundary/UI | NOT RUN | Long profile values tested, but exact chat-list combination not executed | — |
| IOS-041 | Chat list/Profile | Missing avatar | P1 | Negative/UI | NOT RUN | Dedicated missing-avatar scenario not executed | — |
| IOS-042 | Chat list | Unread boundaries 1/9/99/100/999 | P1 | Boundary/UI | NOT RUN | Normal unread behavior verified; full matrix not executed | — |
| IOS-043 | Profile | Empty optional fields | P1 | Negative/UI | PASS | Partially empty profile opens safely | — |
| IOS-044 | Profile | Long profile values | P1 | Boundary/UI | PASS | Long values remain displayable; no critical layout break observed | — |
| IOS-045 | Navigation | Rapid repeated taps | P1 | Negative/Stability | PASS | No duplicate entities/screens observed | — |
| IOS-046 | Navigation | Rapid back during transitions | P1 | Stability | NOT RUN | Dedicated transition-timing scenario not executed | — |
| IOS-047 | Persistence | Immediate force-close after send | P0 | Boundary/Persistence | NOT RUN | Exact immediate-kill timing not executed | — |
| IOS-048 | Offline | Cold launch without network | P0 | Offline/Functional | PASS | Local chats/data remain available offline | — |
| IOS-049 | Offline | Send + wallpaper + restart fully offline | P0 | Offline/Persistence | NOT RUN | Full chained offline scenario not executed | — |
| IOS-050 | Privacy/Isolation | Reject all unrelated permissions | P0 | Privacy/Isolation | NOT RUN | Full permission-denial regression not executed | — |
| IOS-051 | Hidden editor | Wrong-zone / short-hold negative | P2 | Optional/Negative | NOT RUN | Gesture-negative matrix not executed | — |
| IOS-052 | Hidden editor | Cancel edit without save | P2 | Optional/Negative | PASS | Previous value remains unchanged | — |
| IOS-053 | Hidden editor | Empty/invalid/long editor values | P2 | Optional/Validation | NOT RUN | Values explored, but no formal validation contract existed | — |
| IOS-054 | Backup | Import valid JSON | P2 | Optional/Import | NOT RUN | Not executed | — |
| IOS-055 | Backup | Import malformed JSON | P2 | Optional/Negative | NOT RUN | Not executed | — |
| IOS-056 | Backup | ~50 MB import boundary | P2 | Optional/Boundary | NOT RUN | Not executed | — |
| IOS-057 | Backup | Export JSON + re-import | P2 | Optional/Import-Persistence | NOT RUN | Not executed | — |
| IOS-058 | Messaging | Reply retains source context | P2 | Functional/UI | FAIL | Reply sends as ordinary message without source context | BUG-03 |
| IOS-059 | Message interaction | Destructive action from selected message | P2 | Functional/UX | FAIL | Whole-chat delete action is available from single-message context | BUG-02 |
| IOS-060 | Own profile | Edit own profile | P1 | Functional/Stability | FAIL | Name/birth date/avatar save hangs on endless loader | BUG-04 |
| IOS-061 | Profile | Open fully empty correspondent profile | P1 | Negative/Stability | FAIL | App terminates; reproduced 2/2 with matching crash signature | BUG-05 |

## Acceptance mapping

The mandatory acceptance result is **8 / 9 fully passed**.

- IOS-018 / BUG-01 is the only direct failure among the nine mandatory checks.
- IOS-058–061 are additional exploratory/optional defects discovered beyond the mandatory acceptance list.

## Defect traceability

| Failed case | Defect |
|---|---|
| IOS-018 | [BUG-01](../bugs/BUG_REPORTS.md#bug-01--partial-message-text-selection-is-unavailable) |
| IOS-058 | [BUG-03](../bugs/BUG_REPORTS.md#bug-03--reply-loses-source-message-context) |
| IOS-059 | [BUG-02](../bugs/BUG_REPORTS.md#bug-02--whole-chat-delete-is-exposed-from-single-message-context) |
| IOS-060 | [BUG-04](../bugs/BUG_REPORTS.md#bug-04--editing-own-profile-hangs-on-endless-loader) |
| IOS-061 | [BUG-05](../bugs/BUG_REPORTS.md#bug-05--fully-empty-correspondent-profile-causes-application-crash) |

## Evidence mapping

The original private delivery included screenshots for BUG-01/BUG-02 and live syslog + two native `.ips` reports for BUG-05.

Public handling and evidence rationale: [evidence/README.md](../evidence/README.md).
