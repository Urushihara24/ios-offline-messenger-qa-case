# Test Environment

## Device

- Physical device: **iPhone 13** (`iPhone14,5`)
- OS: **iOS 18.2**
- Test type: real-device manual testing

## Application build

- App version: **13.1.1**
- Build: **17**
- Installation: sideloaded/development-signed test build
- Isolation: dedicated bundle identifier, separate from the installed real Telegram application

## Tooling used during the QA session

- `libimobiledevice` / `idevice*` tooling for device communication and logs
- `idevicesyslog` for live runtime logging
- iOS `.ips` crash reports for post-crash analysis
- command-line inspection of crash-report JSON
- Google Sheets / Docs for execution tracking and delivery artifacts

## Environment-specific verification

The following were explicitly checked:

- the real Telegram app and the simulator can coexist on the same device;
- the simulator does not expose or reuse the real Telegram application's chats or profile data;
- repeated cold starts of build 17 are stable;
- local functionality remains available without network access;
- sent messages and wallpaper selection persist after a full application restart.

## Previous-build regression context

An earlier build exhibited repeated startup crashes. Build 17 was therefore treated as a regression candidate and repeatedly cold-started before functional acceptance testing continued.

The public case does not include previous-build raw crash artifacts because the goal is to document the QA decision path, not to publish client runtime data.
