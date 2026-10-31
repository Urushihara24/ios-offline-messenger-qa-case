# Test Plan & Scope

## Product under test

A local/offline iOS messenger simulator with a Telegram-like interface. The test build uses its own application container and local data store. No real account, backend session, or synchronization is required for the covered scenarios.

## Test objectives

- validate the nine mandatory acceptance requirements;
- verify that the local messenger flow works on a physical iPhone;
- confirm persistence after full application restart;
- verify offline behavior and application-data isolation;
- exercise the optional hidden editor used to prepare local demo data;
- extend coverage with exploratory, negative, boundary, and stability checks;
- capture and investigate reproducible runtime failures without overstating root cause.

## Mandatory acceptance scope

1. **Chat list** — avatar, name, last-message preview, time, unread counter.
2. **Chat screen** — message history, dates/times, one/two checkmarks for outgoing messages.
3. **Correspondent status** — online, recently seen, animated typing state.
4. **Send message** — input clears and the outgoing message appears in the chat.
5. **Correspondent profile** — avatar, first name, last name, username, About, phone.
6. **Message interaction** — context menu and standard text selection.
7. **Settings** — final tab is settings; own profile image/data are visible.
8. **Chat wallpapers** — change wallpaper, return to chat, verify change, restore default.
9. **Persistence** — sent messages and selected wallpaper survive a full application restart.

## Optional hidden-editor scope

The service editor is opened by a long press in the top-center/title area. It was used to create and modify local test data:

- own profile;
- correspondents;
- chats;
- messages;
- dates and timestamps;
- message checkmarks;
- correspondent statuses;
- unread values.

The editor is optional scope and does not change the mandatory 8/9 acceptance result.

## Exploratory extensions

Additional coverage included:

- multiple-chat and correspondent isolation;
- edit/delete persistence;
- cancellation of unsaved changes;
- rapid repeated actions and duplicate prevention;
- empty and whitespace-only message behavior;
- emoji-only, multiline, and long text;
- long profile values;
- avatar replacement;
- offline cold launch and local functionality;
- coexistence with the real Telegram application;
- isolation from the real Telegram application's data;
- regression checks after startup crashes observed in an earlier build.

## Planned but not fully executed

The final suite retains several `NOT RUN` scenarios rather than presenting them as passed coverage. These include:

- exact 1-character message boundary;
- full 255 / 256 / 1000 / 10000 character matrix;
- full Unicode/ZWJ modifier matrix;
- unread boundaries 1 / 9 / 99 / 100 / 999;
- immediate force-close timing after send;
- full permission-denial regression;
- JSON import/export and ~50 MB file boundary checks.

See [TEST_CASES.md](../test_cases/TEST_CASES.md) for the execution matrix.

## Explicitly outside scope

The following features were not required and were not classified as defects when absent:

- login, registration, and SMS flows;
- calls;
- groups, channels, and bots;
- search for external users or chats;
- stories playback;
- cloud synchronization;
- push notifications.

## Entry criteria

- build installed on a physical test device;
- application launches successfully;
- test data can be prepared locally;
- real Telegram remains independently installed for isolation checks.

## Exit criteria

- all nine mandatory acceptance items receive a final PASS/FAIL result;
- reproducible failures are recorded as defect reports;
- high-impact stability defects include technical evidence where available;
- unexecuted expanded scenarios remain explicitly marked `NOT RUN`.

## Public-case sanitization

This repository omits client-identifying data, raw device/signing identifiers, raw syslog, and raw `.ips` files. The public version preserves scope, execution logic, traceability, and technical conclusions without exposing sensitive runtime artifacts.
