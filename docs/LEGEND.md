# QA Legend

## Execution status

| Status | Meaning |
|---|---|
| `PASS` | Executed; actual result matches the expected result |
| `FAIL` | Executed; actual result differs from the expected result |
| `BLOCKED` | Execution could not be completed because of an external blocker |
| `NOT RUN` | Planned coverage not executed in this test cycle |

`NOT RUN` is intentionally preserved instead of being converted into a synthetic PASS. This matters in this case because several expanded boundary/import scenarios were planned but were outside the mandatory acceptance run.

## Priority

| Priority | Meaning |
|---|---|
| `P0` | Core/smoke path; failure threatens basic use or acceptance |
| `P1` | Important functional or stability issue that should be fixed before final acceptance |
| `P2` | Secondary/optional/UX issue with lower acceptance impact |

## Severity

| Severity | Meaning |
|---|---|
| High | Crash, severe loss of usability or major stability impact |
| Medium | Clear functional mismatch or significant UX/workflow failure without total application loss |
| Low | Minor cosmetic or limited-impact defect |

## Evidence policy

Raw client screenshots, syslog and `.ips` files are kept out of this public repository. Public documents preserve:

- reproduction steps;
- actual vs expected behavior;
- test-case ↔ bug mapping;
- sanitized crash signature;
- evidence type and QA conclusion.
