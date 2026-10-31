# Crash Analysis — Empty Correspondent Profile

## Summary

A deterministic application crash was reproduced when opening a correspondent profile after all profile data had been removed through the hidden service editor.

The defect was reproduced twice on the same physical device and build. Both `.ips` reports produced the same exception type, faulting thread and application-frame offsets.

## Reproduction path

1. Open the hidden service editor.
2. Remove all available data from one correspondent profile.
3. Save the edited state.
4. Open the dialog with that correspondent.
5. Tap the correspondent name/profile in the chat header.
6. Observe the application terminate.

## Reproduction result

| Run | Build | Result |
|---|---|---|
| 1 | 17 | Crash |
| 2 | 17 | Crash |

**Reproducibility:** 2 / 2.

## Sanitized crash signature

```text
Exception: EXC_BREAKPOINT
Signal: SIGTRAP
Termination: Trace/BPT trap: 5
Faulting thread: 0

Top application image:
TelegramUIFramework

Repeated downstream application image:
SwiftSignalKitFramework

Signature comparison:
identical across both captured reports
```

## What the crash reports prove

The captured evidence supports the following conclusions:

- the crash is not a one-off UI freeze or manual termination;
- both reproductions belong to the tested build;
- both failures terminate with the same exception/signal combination;
- both reports identify the main thread as the faulting thread;
- the same application frameworks and frame offsets appear in both reports;
- the failure is therefore stable enough to hand off as a reproducible crash defect.

## What was deliberately **not** claimed

No exact source function, Swift statement or root cause was assigned.

The crash reports were not symbolicated with the matching dSYM. Without symbols, frame offsets can identify a stable signature and the involved binary image, but not a defensible source-level cause.

A statement such as “empty data causes a nil unwrap” would therefore be speculation, not evidence.

## Developer handoff recommendation

For source-level diagnosis:

1. obtain the dSYM matching the application/framework UUIDs from build 17;
2. symbolicate the faulting `TelegramUIFramework` frames;
3. inspect profile construction/rendering for the fully empty profile state;
4. add a defensive empty-state/default-profile path;
5. rerun the exact reproduction scenario and a regression matrix for partially empty profiles.

## Evidence handling

The original QA delivery included:

- live syslog captured during reproduction;
- two independent `.ips` crash reports;
- timestamp correlation with the manual reproduction.

Those raw files are intentionally excluded from this public repository because they may contain device, filesystem, signing or client runtime metadata.
