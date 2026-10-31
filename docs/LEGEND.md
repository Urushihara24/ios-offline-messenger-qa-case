# QA Legend

## Execution status

| Status | Meaning |
|---|---|
| `PASS` | Executed; Actual matches Expected |
| `FAIL` | Executed; Actual differs from Expected |
| `BLOCKED` | Execution could not be completed because of an external blocker |
| `NOT RUN` | Planned coverage not executed in this test cycle |

`NOT RUN` is intentionally preserved rather than converted into a synthetic PASS. This repository distinguishes planned coverage from executed coverage.

## Severity

| Severity | Meaning |
|---|---|
| High | Crash, severe stability failure, or major loss of usability |
| Medium | Clear functional mismatch or significant workflow/UX failure without total application loss |
| Low | Minor cosmetic or limited-impact defect |

## Priority

| Priority | Meaning |
|---|---|
| `P0` | Core smoke/acceptance path; failure threatens basic use |
| `P1` | Important functional or stability issue; should be addressed before final acceptance |
| `P2` | Secondary, optional, or UX issue with lower acceptance impact |

## Defect reporting format

Each defect report includes, where applicable:

- ID and title;
- Severity / Priority;
- related test case;
- preconditions;
- reproduction steps;
- Actual result;
- Expected result;
- reproducibility;
- evidence note;
- diagnostic constraints when root cause cannot be proven.

## Traceability

Failed test cases reference the related defect ID. The defect report points back to the corresponding test case.

This keeps three layers separate:

1. **test case** — what was checked;
2. **execution result** — what happened;
3. **defect report** — why the mismatch matters and how to reproduce it.

## Evidence policy

Raw client screenshots, syslog, and `.ips` files are excluded from the public repository. Public documentation preserves:

- reproduction steps;
- Actual vs Expected;
- test-case ↔ defect mapping;
- reproducibility;
- sanitized crash signature;
- evidence type;
- explicit limits on what the evidence can prove.
