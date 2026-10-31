# Crash Analysis — BUG-05

## Incident summary

A deterministic application crash was reproduced when opening a correspondent profile after all profile data had been removed through the hidden service editor.

The failure was reproduced twice on the same physical device and build. Both native `.ips` reports matched on exception type, faulting thread, application frameworks, and frame-offset sequence.

## Reproduction

### Preconditions

- build 17 installed on the physical test device;
- correspondent and chat exist locally;
- all available profile data for that correspondent has been removed through the service editor.

### Steps

1. Open the dialog with the empty-profile correspondent.
2. Tap the correspondent name/profile in the chat header.
3. Observe application behavior.

### Result

| Run | Build | Result |
|---|---|---|
| 1 | 17 | Crash |
| 2 | 17 | Crash |

**Reproducibility:** 2 / 2.

## Captured evidence

The original QA delivery included:

- live syslog captured during the controlled reproduction;
- two independent native `.ips` crash reports;
- manual reproduction timestamps used to correlate the reports with the tested action.

Raw artifacts are excluded from the public repository. See [Evidence Policy](../evidence/README.md).

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

## Evidence-backed conclusions

The captured reports support the following conclusions:

- the failure is a native application crash, not a UI freeze or manual termination;
- both reports belong to the tested build;
- both reproductions terminate with the same exception/signal combination;
- both reports identify the main thread as the faulting thread;
- the same application framework sequence appears in both reports;
- the same frame offsets recur across both reports;
- the defect is stable enough for deterministic developer handoff and regression testing.

## Diagnostic limits

No exact Swift function, source statement, or source-level root cause is claimed.

The matching build-17 dSYM was not available for symbolication. Unsymbolicated frame offsets are sufficient for crash-signature comparison, but they are not sufficient to prove a specific code path.

For example, a statement such as **“the empty profile triggers a nil unwrap”** would be speculation rather than evidence.

## Developer handoff

Recommended next steps:

1. obtain the dSYM matching the application/framework UUIDs from build 17;
2. symbolicate the faulting `TelegramUIFramework` frames;
3. inspect profile construction/rendering for the fully empty state;
4. add a safe empty/default-profile path;
5. retest the exact BUG-05 reproduction;
6. run a regression matrix for partially empty and fully populated profiles.

## QA assessment

**Severity:** High  
**Priority:** P1

The crash does not affect the normal filled-profile acceptance flow, but it is a deterministic stability failure reachable through locally editable test data. It should be fixed before final acceptance of the editor-supported workflow.
