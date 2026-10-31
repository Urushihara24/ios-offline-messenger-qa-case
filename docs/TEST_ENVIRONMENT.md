# Environment & Tools

## Test environment

| Parameter | Value |
|---|---|
| Device | Physical iPhone 13 (`iPhone14,5`) |
| OS | iOS 18.2 |
| Application | 13.1.1, build 17 |
| Installation | Sideloaded / development-signed build |
| Test type | Real-device manual testing |
| Data model | Local/offline application data |
| Isolation | Dedicated application bundle, separate from the installed real Telegram app |

## Tooling

| Tool / artifact | Purpose |
|---|---|
| `libimobiledevice` / `idevice*` | Device communication and iOS diagnostics |
| `idevicesyslog` | Live runtime log capture during controlled reproduction |
| iOS `.ips` reports | Native crash evidence |
| Python / CLI JSON inspection | Crash-report field extraction and signature comparison |
| Google Sheets | Test-case execution and defect traceability |
| Google Docs | Final QA delivery report |
| GitHub | Sanitized public portfolio documentation |

## Environment-specific verification

The following checks were performed explicitly:

- the real Telegram application and the simulator can coexist on the same device;
- the simulator does not expose or reuse the real Telegram application's chats or profile data;
- repeated cold starts of build 17 are stable;
- local chat functionality remains available without network access;
- sent messages persist after a full application restart;
- selected wallpaper persists after a full application restart.

## Regression context

An earlier build exhibited repeated startup crashes. Build 17 was therefore treated as a regression candidate before the functional acceptance run continued.

Repeated cold starts on build 17 did not reproduce the earlier startup failure, which helped separate the resolved launch-stability problem from the later profile-specific crash documented as BUG-05.

## Evidence handling

The original QA delivery included raw device-side artifacts where needed. The public repository intentionally keeps only sanitized conclusions and traceability because raw syslog and `.ips` files can expose device, container, signing, and client runtime metadata.
