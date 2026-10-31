# Test Scope

## Product under test

A local/offline iOS messenger simulator with a Telegram-like interface. The build uses its own bundle identifier and local application data. No real account, backend session or synchronization is required for the tested scenarios.

## Mandatory acceptance scope

1. **Chat list** — avatar, name, last-message preview, time and unread counter.
2. **Chat screen** — message history, dates/times and one/two checkmarks for outgoing messages.
3. **Correspondent status** — online, recently seen and animated typing state.
4. **Send message** — input clears and the outgoing message appears in the chat.
5. **Correspondent profile** — avatar, first name, last name, username, About and phone.
6. **Message interaction** — context menu plus standard text selection.
7. **Settings** — final tab is settings; own profile image/data are visible.
8. **Chat wallpapers** — change wallpaper, return to chat, verify change, restore default.
9. **Persistence** — sent messages and selected wallpaper survive a full application restart.

## Optional service-editor scope

The hidden editor is opened by a long press in the top-center/title area. It was used to create and modify local test data:

- own profile;
- correspondents;
- chats;
- messages;
- dates and timestamps;
- message checkmarks;
- correspondent statuses;
- unread values.

## Exploratory extensions

Additional checks covered:

- multiple chats and correspondent isolation;
- delete and edit persistence;
- cancellation of unsaved edits;
- rapid repeated actions and duplicate prevention;
- empty/whitespace message behavior;
- emoji, multiline and long text;
- long profile values;
- avatar replacement;
- offline cold launch and local functionality;
- coexistence with the real Telegram application;
- isolation from the real Telegram application's data.

## Explicitly outside scope

The following features were not required and were not classified as defects when absent:

- login, registration and SMS flows;
- calls;
- groups, channels and bots;
- search for external users or chats;
- stories playback;
- cloud synchronization;
- push notifications.

## Public-case sanitization

This repository intentionally omits client-identifying information, raw device identifiers, signing-team data, raw syslog and raw `.ips` files. Technical conclusions are preserved without publishing sensitive runtime evidence.
